# Règles de sécurité — Bon App’

Ces règles définissent les exigences minimales de sécurité à appliquer pendant la conception,
le développement et l’exploitation du MVP. Elles complètent les
[règles d’architecture](../architecture/architecture-rules.md), les
[conventions de développement](../architecture/coding-conventions.md) et la
[pile technique](../architecture/technology-stack.md). Elles ne remplacent pas une analyse
juridique, un modèle de menace ni les décisions de sécurité propres aux fournisseurs retenus.

## Principes de sécurité

- **Privé par défaut :** les recettes, espaces familiaux et médias ne sont accessibles qu’aux
  personnes authentifiées et autorisées. Le partage doit résulter d’une action explicite et
  révocable.
- **Défense en profondeur :** valider les entrées, contrôler les permissions côté serveur,
  limiter les privilèges et protéger les données à chaque frontière. Une validation ou un
  contrôle dans le client n’est jamais une barrière de sécurité suffisante.
- **Minimisation :** collecter, transmettre, journaliser et conserver uniquement les données
  nécessaires au fonctionnement défini.
- **Échec sûr :** en cas de configuration absente, d’identité incertaine ou de contrôle d’accès
  impossible, refuser l’opération plutôt que d’accorder un accès par défaut.
- **Traçabilité maîtrisée :** conserver les événements nécessaires à l’exploitation et à la
  sécurité sans inscrire le contenu privé ni des secrets dans les journaux.

## Classification des données

Classer les données selon leur sensibilité et appliquer le niveau le plus élevé lorsqu’un
enregistrement contient plusieurs catégories.

| Niveau | Exemples Bon App’ | Règles minimales |
|---|---|---|
| **Public** | Contenu explicitement publié par Bon App’ pour tous ; documentation sans détails opérationnels sensibles | Peut être partagé publiquement après validation éditoriale. Ne doit pas contenir de données personnelles ou de détails internes par défaut. |
| **Interne** | Documentation de travail non publique, configuration non secrète, métriques agrégées non identifiantes | Accès limité à l’équipe et aux outils approuvés ; ne pas publier dans un dépôt public ni transmettre à un service externe sans motif. |
| **Confidentiel** | Recettes privées, variantes, commentaires, photos, vidéos, notes vocales, courriels, identifiants de compte, données d’usage liées à un utilisateur | Accès au besoin et selon les permissions ; chiffrement en transit et au repos ; pas de copie vers des environnements ou services non approuvés. |
| **Restreint** | Mots de passe, jetons de session, clés API/privées, credentials cloud, secrets de signature, sauvegardes contenant des données confidentielles, données d’authentification permettant une prise de compte | Accès strictement limité aux services/personnes autorisés ; stockage dans un gestionnaire de secrets ; jamais dans les clients, prompts, journaux, tickets ou dépôts. |

Une recette ou un média est **confidentiel**, même s’il ne contient pas de nom ; une photo ou
note vocale peut également révéler des informations personnelles incidentes. Un contenu rendu
public par son propriétaire ne devient public qu’après une action explicite et ne modifie pas
la classification des copies, sauvegardes ou données liées à d’autres personnes.

## Identité, sessions et contrôle d’accès

- Toute opération protégée est authentifiée et autorisée par l’API. Les clients ne décident
  jamais seuls qu’un utilisateur peut lire ou modifier une recette.
- Les routes de lecture publique ne sont autorisées que si elles sont explicitement conçues
  comme telles ; toutes les autres routes exigent une identité valide. Aucune identité ou session
  anonyme n’obtient implicitement accès à des données privées.
- L’API vérifie cryptographiquement les jetons d’identité avec l’émetteur attendu, l’audience, la
  signature, les dates de validité et les algorithmes autorisés. Elle refuse les jetons absents,
  expirés, mal formés, révoqués lorsque la vérification est disponible, ou émis pour un autre
  service. Ne jamais faire confiance à des claims fournis séparément par le client.
- Vérifier l’autorisation pour chaque ressource et action, y compris les recettes, variantes,
  commentaires, espaces et médias. Ne pas s’appuyer uniquement sur un identifiant opaque ou un
  identifiant fourni par le client.
- Appliquer le contrôle d’accès selon le propriétaire, l’appartenance active à l’espace familial,
  le rôle, l’action demandée et l’état de partage. Revérifier l’appartenance lors de chaque
  opération ; une ancienne invitation, un rôle retiré ou la connaissance d’un identifiant
  n’accorde aucun droit.
- Refuser par défaut lorsque la ressource, l’identité ou la relation d’accès n’est pas vérifiable.
  Les listes et recherches doivent être filtrées côté serveur par les ressources accessibles.
- Ne pas révéler l’existence ou le contenu d’une ressource privée à un utilisateur non autorisé ;
  les réponses d’erreur ne doivent pas permettre de contourner les permissions.
- Protéger les opérations sensibles (connexion, récupération de compte, invitation, partage,
  changement de rôle et révocation) contre les abus, la répétition et l’énumération de comptes.
- Ne pas implémenter de mécanisme cryptographique de mot de passe, session ou jeton maison. Avant
  tout lancement, choisir un fournisseur ou adopter une bibliothèque et un protocole éprouvés par
  ADR. Définir alors les exigences de mots de passe, session, durée, renouvellement, révocation,
  récupération, MFA et gestion des comptes.
- La décision d’authentification doit préciser le mécanisme de credential utilisé par le web et
  les clients natifs, la durée maximale des sessions, leur renouvellement et leur révocation.
- Si le web utilise des cookies d’authentification, les marquer `Secure` et `HttpOnly`, choisir
  `SameSite` explicitement et protéger toutes les opérations modifiant l’état contre les CSRF
  (jeton anti-CSRF et vérification de l’origine, ou protections équivalentes validées). Le CORS
  n’autorise que les origines nécessaires et ne combine jamais credentials avec une origine
  générique. Les tests doivent confirmer le rejet des requêtes inter-origines non autorisées.
- Ne jamais stocker de jeton d’accès dans un emplacement client accessible à du code non fiable
  sans évaluation de la plateforme et décision documentée. Ne jamais journaliser des jetons.

## API et validation des entrées

- Traiter toute requête, fichier, en-tête, paramètre, réponse de fournisseur et donnée importée
  comme non fiable. Valider format, taille, plage et valeurs autorisées à l’exécution.
- Valider en liste positive : rejeter les champs inconnus lorsqu’ils peuvent affecter les
  permissions ou les données persistées ; ne jamais assigner aveuglément le corps reçu à un
  modèle de base. Les champs modifiables sont explicitement autorisés par opération.
- Définir pour chaque champ son type, présence, longueur minimale/maximale, format, plage,
  encodage et normalisation. Valider les dates, nombres, tableaux et enums sans conversions
  permissives ou perte de précision. Les types TypeScript n’effectuent pas de validation à
  l’exécution.
- Échapper les données selon leur contexte de sortie (HTML, URL, SQL, shell) et préférer les API
  qui séparent données et instructions. Le HTML enrichi est interdit sauf besoin approuvé, avec
  assainissement dédié.
- Vérifier les règles métier après validation de forme : cohérence des unités, existence des
  relations, état de l’invitation, droits sur l’espace et transitions d’état permises.
- Utiliser des requêtes paramétrées. Les noms de colonnes, tris, filtres, chemins de stockage et
  autres éléments non paramétrables sont sélectionnés dans une liste autorisée.
- Limiter les tailles de requêtes, fichiers, listes et résultats ; appliquer des délais d’attente
  et des limites de débit appropriées aux opérations exposées. Configurer des limites distinctes
  pour l’authentification, les invitations, l’import média, la recherche et les API publiques ;
  fixer les seuils chiffrés avant mise en production et les tester.
- Protéger les opérations contre les répétitions dangereuses et les abus. Les opérations
  susceptibles de créer des doublons doivent définir une stratégie d’idempotence.
- Retourner des erreurs utiles mais non révélatrices. Exclure les traces d’exécution, requêtes,
  noms de secrets, détails de fournisseurs et informations sur d’autres comptes.
- Ne pas activer de mécanisme de partage public ou de lien durable avant d’avoir défini son
  expiration, sa révocation, son périmètre et les avertissements présentés à l’utilisateur.

## Médias et stockage objet

- Stocker les photos, vidéos et notes vocales dans un stockage objet privé compatible S3 ; ne
  jamais rendre un bucket ou un objet public par défaut.
- L’API vérifie les permissions avant de délivrer un accès temporaire ou d’autoriser un transfert.
  Les clés permanentes du fournisseur restent côté serveur et ne sont jamais intégrées dans les
  applications web ou mobiles.
- Une URL temporaire est limitée à un seul objet et à une seule opération (lecture ou écriture),
  avec une expiration maximale de cinq minutes. Elle ne permet jamais de lister ou supprimer des
  objets. Pour les transferts, imposer également le type et la taille autorisés lorsque le
  fournisseur le permet ; sinon, transférer via l’API ou un mécanisme offrant ces garanties.
  Tester l’expiration, ainsi que l’impossibilité d’utiliser l’URL pour un autre objet ou une
  autre opération. Une copie déjà téléchargée par un utilisateur ne peut pas être révoquée par
  l’expiration de l’URL.
- Utiliser des identifiants d’objet générés ou validés côté serveur. Ne pas accepter un chemin
  arbitraire fourni par le client comme preuve d’accès ou de propriété.
- Valider le type réel, le format, la taille et le nom des fichiers. Ne pas se fier uniquement à
  l’extension ou au `Content-Type` déclaré. Les formats autorisés et les limites doivent être
  définis avant l’implémentation du téléversement.
- Empêcher l’exécution de contenu téléversé ; servir les fichiers avec des types et en-têtes
  sûrs et selon le besoin produit. Évaluer l’analyse antimalware et le nettoyage des métadonnées
  des images avant mise en production.
- Définir les règles de suppression et de rétention de façon cohérente entre les métadonnées
  PostgreSQL, les fichiers stockés, les sauvegardes et les accès temporaires. Prévoir le
  nettoyage des objets orphelins après échec d’un transfert ou d’une suppression.
- Ne pas transmettre de médias privés à un service OCR, d’image ou autre fournisseur sans
  fournisseur approuvé, finalité définie, information/consentement appropriés et évaluation du
  traitement des données.

## Données personnelles et confidentialité

- Ne collecter que les informations nécessaires aux comptes, recettes, espaces et fonctions
  effectivement livrées. Éviter les données sensibles qui ne sont pas indispensables au produit.
- Restreindre l’accès aux données en fonction des besoins métier et éviter de dupliquer les
  données personnelles dans des caches, exports ou environnements de test.
- Utiliser des données fictives ou anonymisées en développement et en test. Ne pas copier des
  recettes, médias, comptes ou sauvegardes de production vers des environnements non autorisés.
- Chiffrer les échanges réseau. Activer et vérifier le chiffrement au repos des services retenus ;
  les responsabilités de gestion et de rotation des clés doivent être définies.
- Utiliser TLS 1.2 ou supérieur pour les communications réseau ; désactiver les protocoles et
  suites cryptographiques obsolètes. Les connexions internes entre services et bases ne sont pas
  exemptées du chiffrement lorsqu’elles traversent un réseau non fiable.
- Activer le chiffrement au repos pour PostgreSQL, les médias, les sauvegardes, les exports et
  les volumes contenant des données confidentielles. Privilégier le chiffrement géré par le
  fournisseur approuvé ; les clés ne sont jamais stockées avec les données qu’elles protègent.
- Ne pas concevoir d’algorithme cryptographique maison ni réutiliser une clé entre environnements
  ou usages. Définir propriétaire, accès, rotation, révocation et procédure de récupération des
  clés avant production. Les exigences de chiffrement applicatif de bout en bout restent à décider
  selon les besoins et ne sont pas implicitement garanties par le chiffrement au repos.
- Définir et documenter les finalités, durées de conservation, procédures d’export et de
  suppression, règles de consentement et mécanismes de réponse aux demandes des personnes avant
  le lancement public.
- Évaluer les transferts de données vers les fournisseurs (région, sous-traitants, rétention,
  accès et conditions contractuelles) avant leur autorisation. Ne pas prétendre à une conformité
  réglementaire sans évaluation adaptée.

## Données interdites dans les prompts

Cette règle s’applique aux prompts, instructions, messages, pièces jointes et contextes transmis
à un modèle d’IA, assistant de code ou service externe de génération/analyse, y compris pour
l’OCR, la structuration de recettes, le débogage et le support.

- **Interdit en toutes circonstances :** données de niveau Restreint (mots de passe, jetons,
  clés, credentials, codes de récupération, secrets de signature, secrets de production) et
  données permettant de contourner l’authentification ou les permissions.
- **Interdit sans décision de sécurité préalable :** tout contenu Confidentiel, notamment
  recettes privées, commentaires, médias, notes vocales, texte OCR issu de médias privés,
  courriels, identifiants de compte, données personnelles ou tickets contenant ces éléments.
- Ne pas transmettre de dépôts, journaux, captures d’écran, exports ou fichiers réels qui
  pourraient contenir secrets ou données utilisateur. Remplacer par des exemples synthétiques,
  minimisés et non ré-identifiants ; supprimer les métadonnées et noms réels.
- Les données Publiques ou Internes peuvent être utilisées uniquement si le service est approuvé
  pour cet usage et si le contenu ne révèle pas de secret, vulnérabilité non publiée ou détail
  opérationnel sensible.
- Une exception pour une fonction produit (par exemple l’OCR d’une recette à la demande de son
  propriétaire) exige une ADR ou décision de sécurité indiquant fournisseur, finalité, données,
  base de traitement/consentement, région, rétention, usage pour entraînement, contrôle d’accès,
  risques et mécanisme de suppression. N’envoyer que les champs indispensables.
- Avant tout envoi autorisé, vérifier que les prompts n’intègrent pas de données issues d’un autre
  utilisateur ou espace, que l’utilisateur est informé et que le fournisseur ne conserve ni ne
  réutilise le contenu au-delà des conditions approuvées.
- Les prompts et réponses ne doivent pas être conservés dans les logs applicatifs ou analytiques,
  sauf décision explicitement approuvée avec minimisation, accès contrôlé et durée de rétention.

## Secrets et configuration

- Ne jamais versionner de mot de passe, clé privée, jeton, credential cloud, URL contenant un
  secret ou dump de configuration sensible.
- Charger les secrets depuis un gestionnaire ou mécanisme sécurisé de l’environnement serveur.
  Séparer dev, test, staging et production ; ne jamais réutiliser un secret de production ailleurs.
- Donner à chaque service et workflow des identifiants séparés au moindre privilège. Préférer des
  credentials courts ou fédérés aux clés statiques lorsqu’ils sont disponibles ; limiter audience,
  permissions et durée de vie.
- Valider au démarrage les variables obligatoires sans afficher leur valeur dans les erreurs ou
  les logs. Une valeur de sécurité manquante ou invalide doit empêcher le service de démarrer.
- Considérer toute valeur intégrée dans un bundle web/mobile comme publique, même si elle est
  nommée « secret ». Les clients ne reçoivent que les identifiants explicitement publics.
- Restreindre l’accès aux secrets, documenter leur propriétaire et définir leur rotation et leur
  révocation. Révoquer rapidement tout secret exposé, rechercher son usage non autorisé et
  remplacer les copies affectées ; ne pas supprimer l’incident de l’historique sans traiter la
  compromission.
- Les secrets ne figurent ni dans les arguments de commande, ni les URL, messages de commit,
  tickets, prompts, artefacts CI, rapports de test ou dumps. Masquer les valeurs dans toute
  sortie de diagnostic.

## Dépendances et chaîne d’approvisionnement

- Ajouter une dépendance uniquement après justification et revue : maintenance, licence,
  vulnérabilités connues, compatibilité, provenance, accès système/réseau, taille et données
  éventuellement traitées.
- N’ajouter que des dépendances nécessaires, maintenues, avec licence et provenance vérifiables.
  Examiner l’arbre transitif, les scripts d’installation, les permissions, les vulnérabilités et
  les données auxquelles la dépendance peut accéder. Refuser toute dépendance compromise,
  abandonnée sans justification ou issue d’une source mutable/non vérifiable.
- Préférer les bibliothèques et mécanismes déjà retenus ; ne pas ajouter de doublon pour
  l’authentification, la cryptographie, la validation, les requêtes SQL ou le traitement des
  fichiers sans ADR.
- Verrouiller les versions avec le lockfile ; examiner les changements proposés par Dependabot
  et les alertes avant fusion. Traiter les vulnérabilités selon leur exploitabilité et impact ;
  aucune vulnérabilité critique ou élevée exploitable ne peut être livrée sans correction ou
  exception formellement acceptée avec mesures compensatoires, responsable et échéance.
- Produire et conserver un inventaire des dépendances et versions via les outils disponibles.
  Vérifier les mises à jour de sécurité et retirer les dépendances inutilisées.
- Référencer les GitHub Actions par SHA de commit complet et limiter leurs permissions au
  strict nécessaire. Réviser les actions tierces et leur maintenance avant usage.
- Ne pas rendre de secrets accessibles aux workflows déclenchés par des contributions non
  fiables. Séparer les jobs de validation sans secret des jobs de déploiement protégés par
  environnement et approbation.
- Exécuter les vérifications de types, tests et contrôles de sécurité configurés sur les pull
  requests. Le job de sécurité échoue et bloque la fusion en présence d’un secret confirmé dans
  le changement ou d’une vulnérabilité critique/élevée confirmée dans une dépendance utilisée.
  Les faux positifs ou exceptions doivent être évalués, documentés, approuvés et assortis de
  mesures compensatoires et d’une échéance ; ils ne sont pas supprimés silencieusement.
- Exiger la réussite des contrôles CI et une revue avant fusion dans les règles de protection de
  branche. Les workflows de déploiement sont distincts des vérifications de pull request et
  requièrent un environnement protégé avec approbation.
- Ne pas télécharger ou exécuter des scripts depuis des URLs mutables sans version, intégrité et
  origine vérifiables.

## Journalisation, surveillance et réponse aux incidents

- Utiliser le logger structuré approuvé ; ne jamais écrire de mots de passe, jetons, secrets,
  médias, contenu privé de recette ou données personnelles non nécessaires.
- Journaliser les événements de sécurité utiles : échecs d’authentification et limitations
  déclenchées, refus d’accès, changements de rôles/permissions, invitations, partages, révocations,
  actions administratives et changements de configuration sensibles. Inclure horodatage UTC,
  type d’événement, résultat, composant et identifiant de corrélation ; inclure un identifiant
  utilisateur pseudonymisé seulement si nécessaire.
- Ne jamais journaliser corps ou en-têtes complets de requêtes, cookies, jetons, mots de passe,
  prompts/réponses, contenu de recette, nom de fichier privé ou URL d’accès temporaire. Masquer
  les identifiants directs et paramètres sensibles avant émission.
- Distinguer les niveaux : `error` pour un échec nécessitant intervention, `warn` pour un événement
  anormal récupéré ou un refus de sécurité pertinent, `info` pour les événements d’audit autorisés,
  `debug` pour un diagnostic temporaire sans donnée confidentielle. Désactiver ou restreindre le
  niveau debug en production.
- Limiter l’accès aux journaux, définir leur durée de conservation et protéger leur intégrité
  selon l’hébergement retenu. Ne pas journaliser une même erreur à chaque couche.
- Définir des alertes, des responsables, des étapes de confinement, de révocation des secrets,
  d’analyse d’impact et de communication en cas d’incident avant la mise en production.
- Conserver des sauvegardes protégées et tester leur restauration ; une sauvegarde non restaurée
  n’est pas une garantie vérifiée.

## Tests de sécurité attendus

- Tester l’accès autorisé et refusé pour chaque rôle et type de ressource ; inclure des tests
  empêchant l’accès à une recette ou un média appartenant à un autre utilisateur ou espace.
- Tester la validation des entrées invalides, les limites de taille, les filtres et tris autorisés,
  et les réponses d’erreur sans fuite de détails.
- Tester les cas de partage, révocation et expiration d’accès temporaire lorsqu’ils seront
  implémentés.
- Si l’authentification web repose sur des cookies, tester le rejet des opérations inter-origines
  sans protection CSRF valide, ainsi que les attributs de cookie et les origines CORS permises.
- Tester qu’une URL temporaire expire au plus tard après cinq minutes et ne donne accès qu’à
  l’objet et à l’opération prévus.
- Vérifier que les fichiers et secrets ne sont pas présents dans les bundles clients, logs,
  réponses API, artefacts de CI ou dépôts.
- Tester la gestion des erreurs et des indisponibilités des fournisseurs, notamment l’absence
  d’accès accordé par défaut et la reprise sûre des opérations.
- Utiliser des contrôles automatisés d’analyse de dépendances et de secrets sur les pull
  requests. Les vulnérabilités critiques/élevées confirmées et les secrets confirmés bloquent la
  fusion ; les exceptions suivent le processus formel décrit ci-dessus.
- La configuration concrète des outils dépend du forfait GitHub et sera consignée avec les
  workflows et règles de protection de branche. Leur exécution et leur caractère bloquant
  doivent être vérifiés avant d’autoriser une mise en production.

## Décisions de sécurité à formaliser

Consigner une ADR ou une décision de sécurité avant toute modification qui :

- choisit ou remplace l’authentification, les sessions, la MFA ou le fournisseur d’identité ;
- change les rôles, permissions, partage, liens publics ou règles d’accès aux espaces ;
- choisit un fournisseur, une région ou un flux de transfert pour l’OCR, les médias, les courriels
  ou un autre service traitant des données utilisateur ;
- change chiffrement, gestion des clés, stockage des secrets, rétention, suppression, sauvegardes
  ou transferts de données ;
- expose une nouvelle surface publique, ajoute une intégration privilégiée ou modifie les
  contrôles de CI/déploiement ;
- accepte une vulnérabilité connue, une exception aux règles de dépendances ou un risque résiduel
  significatif.

Chaque décision de risque doit identifier le contexte, les données et actifs concernés, les
scénarios de menace, les mesures prises, le risque résiduel, le responsable et la date de
réévaluation.

## Points restant à définir

- Modèle de menace, propriétaire de la classification et éventuelles obligations réglementaires.
- Fournisseur et paramètres d’authentification, sessions, MFA et récupération de compte ; le
  mécanisme de credential web et, si des cookies sont retenus, protections CSRF/CORS doivent
  être décidés avant lancement.
- Modèle de rôles et permissions détaillé pour recettes, espaces, partage et médias.
- Fournisseur de stockage S3, région, chiffrement, validation des fichiers, antivirus éventuel
  et cycle de vie. Tout accès temporaire reste limité à un objet/une opération et à cinq minutes
  maximum, indépendamment du fournisseur choisi.
- Fournisseurs OCR et courriels, consentement, régions et données transmises.
- Seuils chiffrés de débit, tailles maximales et délais d’attente ; paramètres de session et
  protections anti-abus selon le fournisseur et le modèle de menace.
- Politique de rétention, export et suppression ; exigences légales et processus de réponse aux
  demandes et incidents.
- Outils d’analyse sécurité CI compatibles avec le forfait GitHub, responsables opérationnels,
  alertes et exercices de restauration. Le seuil bloquant (secret confirmé et vulnérabilité
  critique/élevée confirmée) est défini par les présentes règles ; l’activation et l’obligation
  de réussite des checks restent à configurer et vérifier dans GitHub.
