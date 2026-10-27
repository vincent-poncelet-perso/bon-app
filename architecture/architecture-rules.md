# Règles d’architecture — Bon App’

Ces règles définissent les contraintes de conception du MVP. Elles complètent la
[pile technique](./technology-stack.md) et les
[conventions de développement](./coding-conventions.md). Une règle ci-dessous ne choisit pas
un fournisseur ou un comportement qui demeure explicitement ouvert dans ces documents.

## Principes directeurs

- Concevoir d’abord pour les besoins du MVP : capturer, organiser, retrouver et partager des
  recettes familiales, avec leurs variantes, anecdotes et médias.
- Garder les recettes privées par défaut. Toute exposition ou modification de données doit être
  explicitement autorisée par les règles de partage et les permissions du serveur.
- Favoriser une expérience et des règles métier cohérentes entre web, iOS et Android, sans
  prétendre que les capacités propres à chaque plateforme sont identiques.
- Préférer des frontières simples, explicites et testables. N’introduire ni microservices, ni
  bus d’événements, ni moteur spécialisé sans besoin mesuré et décision d’architecture.
- Préserver la possibilité de changer d’hébergeur lorsque cela ne crée pas de complexité
  disproportionnée ; ne pas construire une abstraction de portabilité sans cas d’usage.

## Vue d’ensemble et frontières

Le système comporte trois responsabilités principales :

1. **Clients Expo** dans `apps/mobile` et `apps/web` : interface, interactions avec l’appareil,
   validation utile à l’expérience et appels à l’API. Le web et le mobile partagent autant que
   possible composants et logique métier compatibles.
2. **API NestJS** dans `apps/api` : point d’entrée serveur, authentification des requêtes,
   autorisation, validation des entrées, règles métier et orchestration des accès aux données et
   aux services externes.
3. **Données** : PostgreSQL conserve les données relationnelles et métadonnées ; un stockage
   objet privé compatible S3 conserve les fichiers médias.

Les clients ne se connectent jamais directement à PostgreSQL et ne détiennent pas de secrets
serveur ou de clés permanentes du stockage objet. Toute opération d’accès aux données partagées
ou persistées côté serveur passe par l’API, qui applique l’authentification et l’autorisation.
Un cache local côté client reste possible dans le cadre des règles de synchronisation définies.

```text
Client Expo (web / iOS / Android)
              |
       API NestJS
          /      \
 PostgreSQL    Stockage objet privé S3
```

Cette vue logique ne présume pas d’un fournisseur d’hébergement, d’une topologie réseau ou d’un
mode de déploiement.

## Couches et responsabilités des modules

Les dossiers ci-dessous expriment des responsabilités ; ils n’imposent pas de créer une couche
ou un paquet sans code ni besoin réel.

- **Client UI** (`apps/mobile`, `apps/web`) : écrans, navigation, état d’interface,
  retours d’erreur et appels aux capacités de l’appareil. Elle ne contient ni accès direct à la
  base de données, ni secret serveur, ni autorité finale sur les permissions.
- **Client Application** : orchestration des interactions utilisateur et transformation des
  résultats API en état d’écran. La logique métier réutilisée par plusieurs applications peut
  être placée dans un paquet partagé si elle n’est pas liée à l’interface ou à une plateforme.
- **Shared Contracts** (`packages/`) : types et règles de sérialisation réellement communs entre
  producteurs et consommateurs. Ils ne contiennent ni logique dépendant de NestJS/React, ni
  modèles de persistance exposés directement.
- **API Controller** : contrôleurs NestJS, gardes et validateurs d’entrée. Cette couche
  authentifie/autorise l’accès, valide le protocole et délègue le cas d’usage ; elle ne porte pas
  les règles métier ni les requêtes SQL.
- **API Application** : cas d’usage qui coordonnent les règles métier, les transactions et les
  ports nécessaires. Elle ne dépend pas des détails de transport HTTP ou d’un SDK fournisseur.
- **Domain** : règles et invariants des recettes, espaces, rôles, partage et médias.
  Cette couche reste indépendante de l’interface, du transport et de la base de données.
- **API Infrastructure** : adaptateurs PostgreSQL, stockage S3 compatible, authentification,
  courriels ou autres fournisseurs approuvés. Elle implémente les interfaces utilisées par les
  cas d’usage et ne décide pas seule des permissions métier.
- **Data Stores** : PostgreSQL et stockage objet privé compatible S3. Ils sont accessibles
  uniquement via les adaptateurs de `API Infrastructure` et ne contiennent pas de logique
  d’autorisation applicative.
- **Tests** : tests unitaires au plus près des modules ; tests d’intégration aux frontières de
  données et de fournisseurs ; tests de bout en bout transverses dans `tests/e2e/`.

Arborescence logique indicative :

```text
bon-app/
├── apps/
│   ├── mobile/
│   │   ├── app/                # Client UI: screens and navigation
│   │   └── src/                # Client Application: client-side use cases
│   ├── web/
│   │   ├── app/                # Client UI: screens and navigation
│   │   └── src/                # Client Application: client-side use cases
│   └── api/                    # NestJS API
│       └── src/
│           └── recipes/        # Example business domain
│               ├── recipes.controller.ts     # API Controller: HTTP validation and delegation
│               ├── recipes.service.ts        # API Application: use cases and orchestration
│               ├── domain/                   # Business rules and invariants
│               └── infrastructure/           # API Infrastructure: database and provider adapters
├── packages/
│   └── recipe-contracts/       # Shared Contracts
└── tests/
    └── e2e/                    # Cross-layer end-to-end flows
```

Cette arborescence illustre la séparation des responsabilités, pas une obligation de créer
tous ces répertoires à l’avance. Les noms et conventions imposés par NestJS et Expo Router
peuvent prévaloir, tant que les frontières et le sens des dépendances restent respectés.
`Data Stores` (PostgreSQL et stockage objet S3) sont des services externes à l’arborescence
applicative, consommés uniquement par `API Infrastructure`.

La structure interne précise de l’API (par exemple l’usage de ports/adaptateurs) peut rester
simple tant qu’elle respecte ces frontières. Ne pas introduire des interfaces sans besoin de
substitution, de test ou de séparation.

## Dépendances autorisées et interdites

La matrice se lit de la couche appelante (ligne) vers la couche utilisée (colonne). `Oui`
signifie autorisé, `Non` interdit et `Conditionnel` permis uniquement via un contrat explicite,
avec la justification et les validations indiquées dans les règles ci-dessous.

| Caller \ Dependency | Client UI | Client Application | Shared Contracts | API Controller | API Application | Domain | API Infrastructure | Data Stores |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Client UI | — | Oui | Oui | Via API | Non | Non | Non | Non |
| Client Application | Non | — | Oui | Via API | Non | Non | Non | Non |
| Shared Contracts | Non | Non | Conditionnel¹ | Non | Non | Non | Non | Non |
| API Controller | Non | Non | Oui² | — | Oui | Non | Non | Non |
| API Application | Non | Non | Conditionnel² | Non | — | Oui | Non | Non |
| Domain | Non | Non | Non | Non | Non | — | Non | Non |
| API Infrastructure | Non | Non | Conditionnel² | Non | Oui, via ports | Conditionnel² | — | Oui |
| Data Stores | Non | Non | Non | Non | Non | Non | Non | — |
| Tests | Oui | Oui | Oui | Oui | Oui | Oui | Oui | Conditionnel³ |

1. Une dépendance entre packages `Shared Contracts` est autorisée si elle est unidirectionnelle,
   documentée et sans cycle. Un package partagé ne dépend jamais d’une application.
2. Autorisé seulement pour des contrats ou types neutres conçus pour le consommateur ; jamais
   pour des détails propres à une application ou à l’infrastructure. `API Application` dépend
   du domaine, tandis que le domaine ne dépend jamais de l’application.
3. Les tests peuvent accéder à des services ou bases de test isolés, jamais aux données ou
   identifiants de production.

`—` indique la même couche et n’est pas une décision de dépendance. `Via API` signifie un appel
au contrat réseau, et non une dépendance de code aux modules d’exécution NestJS.

Vue synthétique du sens de dépendance autorisé :

```text
Client UI ────────────────> Client Application
      └──────────────────> Shared Contracts
Client Application ──────> Shared Contracts
Client UI / Application ─> API Controller via API contract
API Controller ──────────> API Application ────────────> Domain
API Infrastructure ──────> ports définis par API Application et Domain
API Infrastructure ──────> Data Stores
```

- `apps/` peut dépendre des paquets partagés appropriés. `packages/` ne dépend jamais d’une
  application.
- Les clients ne dépendent pas de modules serveur, d’entités de persistance ou de bibliothèques
  uniquement compatibles Node.js. L’API ne dépend pas de code d’interface React Native.
- Le domaine ne dépend ni de NestJS, Expo, PostgreSQL, du stockage S3 ni d’un fournisseur externe.
- Les contrôleurs ne dépendent pas directement des adaptateurs de base ou des SDK de fournisseurs.
  Ils invoquent les cas d’usage ; ceux-ci utilisent les abstractions requises.
- Les adaptateurs d’infrastructure peuvent dépendre des cas d’usage ou de leurs contrats, jamais
  l’inverse. Les dépendances circulaires entre couches ou domaines sont interdites.
- Une dépendance entre domaines est autorisée seulement si elle suit un contrat explicite et ne
  crée pas de cycle. Les détails d’un domaine ne deviennent pas une API interne publique par
  défaut.
- Ne pas ajouter de microservice, base secondaire, bus, cache distribué, framework ou SDK
  fournisseur sans besoin mesuré et ADR acceptée.
- Toute dépendance directe ou transitive doit être compatible avec les versions verrouillées,
  maintenue, licenciée, analysée pour les vulnérabilités et approuvée selon les
  [conventions de développement](./coding-conventions.md). Les dépendances de test et de build
  suivent les mêmes règles.

### Violations typiques à détecter en revue

1. **Accès direct aux données depuis un client** : un écran importe un client PostgreSQL, un
   SDK S3 avec une clé permanente ou un repository serveur. Indices à rechercher : imports de
   pilotes/SDK d’infrastructure dans `apps/web` ou `apps/mobile`, variables secrètes incluses
   dans le bundle, requêtes directes à la base. Le client doit appeler l’API ; l’API vérifie les
   permissions et fournit, si nécessaire, un accès média temporaire.
2. **Contrôleur API couplé à l’infrastructure** : un contrôleur NestJS exécute du SQL ou appelle
   directement le SDK de stockage, d’OCR ou d’authentification. Indices : constructeur qui injecte
   un adaptateur concret dans le contrôleur, requêtes ou appels fournisseurs dans les handlers.
   Le contrôleur valide le protocole et délègue au cas d’usage ; l’infrastructure implémente les
   ports utilisés par celui-ci.
3. **Domaine dépendant d’un framework ou fournisseur** : une règle métier importe NestJS,
   Expo/React, PostgreSQL, un SDK S3 ou un SDK OCR. Indices : imports d’infrastructure dans un
   module de domaine, décorateurs framework appliqués à des règles métier, types de fournisseur
   dans les signatures du domaine. Le domaine doit rester exprimé avec des types et règles
   métier indépendants ; l’adaptateur traduit vers les API techniques.

## Règles des clients

- Les clients affichent les données et orchestrent les interactions ; ils ne sont pas une
  frontière de sécurité. Toute règle de permission est réappliquée par l’API.
- Garder les règles métier partagées indépendantes des composants d’interface et des API de
  plateforme, lorsqu’elles doivent être utilisées sur plusieurs clients.
- Isoler dans des modules dédiés les accès à la caméra, aux fichiers, au partage système, aux
  notifications et aux capacités natives. Fournir un parcours de repli quand une capacité n’est
  pas disponible.
- Ne pas supposer que le navigateur peut lire des messages privés ou accéder à des fichiers sans
  action explicite de l’utilisateur.
- Les clients ne déclarent pas une opération persistée comme réussie avant confirmation par l’API
  ou le mécanisme de synchronisation défini.
- Le cache local sert à l’affichage ou aux besoins hors ligne définis ; il ne remplace pas la
  source de vérité serveur. Les règles de synchronisation, de conflit et de suppression restent
  à décider avant de promettre une disponibilité hors ligne donnée.

## Règles de l’API

- NestJS expose l’interface serveur consommée par les clients. Les contrôleurs traduisent le
  protocole ; les services portent les cas d’usage ; l’accès aux données et aux fournisseurs
  externes reste isolé derrière des modules adaptés.
- Valider toute entrée externe à l’exécution, y compris les paramètres, corps de requêtes,
  fichiers et réponses de fournisseurs. Les types TypeScript ne remplacent pas cette validation.
- Authentifier chaque requête protégée et vérifier l’autorisation pour chaque ressource et action.
  Ne pas déduire l’accès du seul identifiant transmis par le client.
- Appliquer les permissions au niveau de l’API avant de lire, modifier, partager ou supprimer une
  recette, un espace familial ou un média.
- Ne pas exposer les modèles internes de base comme contrat public. Définir des contrats d’API
  explicites et les faire évoluer de manière compatible ; le style, le versionnement et le format
  d’erreur restent à formaliser.
- Les erreurs sont converties en réponses compréhensibles et sans détails internes. Les détails
  de diagnostic restent dans les logs serveur protégés conformément aux conventions de
  développement.
- Ne pas effectuer d’opérations lentes ou externes dans les chemins de requête sans limites de
  temps, gestion des erreurs et mesure de latence.

## Contrats d’API

Le style de l’API, son versionnement et son format d’erreur restent à choisir. Quelle que soit
la solution retenue, les règles suivantes s’appliquent :

- Le contrat est explicite et documenté ; les entrées sont validées à l’exécution et les sorties
  respectent une forme stable. Les types partagés ne remplacent pas la validation serveur.
- Les DTO et réponses sont distincts des entités et modèles internes. Ne jamais sérialiser
  automatiquement une entité de base comme réponse publique.
- Les champs sensibles et internes sont exclus par défaut. Les changements de contrat doivent
  préserver la compatibilité des clients existants ou faire l’objet d’une version/migration
  coordonnée documentée.
- Les ressources sont identifiées par des identifiants opaques ; le serveur contrôle toujours
  l’accès à une ressource indépendamment de la connaissance de son identifiant.
- Les erreurs ont une forme cohérente, un code exploitable par le client et un message sûr pour
  l’utilisateur. Stack traces, requêtes, secrets et détails d’implémentation ne sortent jamais
  de l’API.
- Les opérations de création, mise à jour, suppression et partage définissent leurs effets,
  validations, règles d’autorisation et comportements de répétition. Les opérations sensibles
  aux doublons doivent définir une stratégie d’idempotence.
- Les listes définissent pagination, tri et filtres autorisés ; les limites de taille sont
  imposées côté serveur. Les choix détaillés restent à formaliser dans le contrat API.
- Toute modification d’un contrat partagé client/API est testée et revue avec les consommateurs
  concernés.

## Accès aux données

- Seule l’infrastructure de l’API accède directement à PostgreSQL et au stockage objet. Ni les
  clients, ni les composants de présentation, ni le domaine ne réalisent d’accès direct.
- Les cas d’usage appellent des services d’accès aux données dédiés (repositories ou équivalent)
  au travers d’interfaces adaptées ; les contrôleurs ne construisent pas de requêtes.
- Utiliser des requêtes paramétrées. Les filtres, tris, noms de colonnes et chemins d’objet
  provenant du client sont validés par liste d’autorisation ; ne jamais les concaténer
  directement dans une requête ou une clé de stockage.
- Appliquer le filtrage par propriétaire/espace et l’autorisation côté serveur à toutes les
  lectures et écritures. Une vérification d’accès suivie d’une opération doit éviter les
  fenêtres où l’autorisation ou la propriété pourrait changer sans contrôle.
- Limiter les données retournées au strict nécessaire ; ne pas charger ou exposer des champs
  sensibles lorsque l’appelant n’en a pas besoin.
- Les transactions PostgreSQL couvrent les mises à jour relationnelles qui doivent être
  atomiques. Une transaction ne couvre pas automatiquement un stockage objet ou un fournisseur
  distant : les flux multi-systèmes doivent définir reprise, nettoyage des objets orphelins et
  gestion d’échec avant implémentation.
- Aucun ORM ou outil de migration n’est encore choisi. Son adoption et les conventions de
  requêtes/migrations nécessitent une décision documentée avant intégration.

## Données, cohérence et médias

- PostgreSQL est la source de vérité des entités relationnelles : comptes ou références
  d’identité, espaces, rôles, recettes, ingrédients, étapes, variantes, commentaires et
  métadonnées de médias, selon le modèle de données à définir.
- Le stockage objet privé compatible S3 conserve le contenu binaire des photos, vidéos et notes
  vocales. PostgreSQL conserve les identifiants et métadonnées nécessaires à leur rattachement,
  leurs droits et leur cycle de vie, pas les gros fichiers eux-mêmes.
- Les objets ne sont pas publics par défaut. Le serveur vérifie les permissions avant de délivrer
  un accès temporaire ou d’autoriser une opération de transfert. Les URL temporaires ne doivent
  pas être traitées comme des identifiants permanents.
- Le client ne fournit pas librement les clés d’objet ou les chemins de stockage à utiliser. Le
  serveur génère ou valide les identifiants et contrôle les opérations autorisées.
- Les changements de schéma passent par des migrations versionnées et relues. Les opérations
  multi-entités devant rester cohérentes utilisent une transaction PostgreSQL.
- Les règles détaillées de suppression, rétention, sauvegarde, restauration, quotas, formats
  autorisés et analyse des fichiers doivent être définies avant la mise en production.

## Services externes et traitements asynchrones

- Un fournisseur externe ne devient une dépendance d’exécution qu’après décision documentée,
  examen des coûts, régions et données transmises, et validation de la sécurité et du budget.
- Isoler les intégrations externes derrière une frontière serveur afin que les cas d’usage ne
  soient pas couplés au SDK d’un fournisseur. Ne pas construire une abstraction générique si un
  seul fournisseur et un seul usage sont retenus.
- OCR, structuration sémantique, authentification et courriels, notifications push,
  hébergement et traitement d’image demeurent des décisions ouvertes dans la pile technique.
  Aucun fournisseur ou moteur ne doit être présumé par ce document.
- Distinguer la reconnaissance de texte de son interprétation en ingrédients, quantités, étapes
  ou variantes. Une sortie OCR est une proposition à corriger et confirmer, pas une recette
  structurée réputée exacte.
- N’introduire une file de messages, un ordonnanceur ou un traitement en arrière-plan qu’après
  définition d’un besoin qui ne peut être satisfait simplement dans le flux API, avec garanties
  de reprise, d’idempotence, de visibilité des échecs et de supervision.

## Sécurité, confidentialité et résilience

- Appliquer le moindre privilège aux utilisateurs, services, bases de données, stockages et
  workflows de livraison.
- Ne jamais embarquer de secret serveur dans les clients. Lire les secrets depuis une
  configuration sécurisée côté serveur ; valider la configuration obligatoire au démarrage.
- Minimiser les données personnelles collectées, conservées et journalisées. Ne pas envoyer des
  photos ou recettes privées à un fournisseur externe sans finalité, information et décision
  de traitement établies.
- Utiliser des connexions chiffrées en transit et les mécanismes de chiffrement au repos offerts
  par les environnements retenus ; les clés et leur rotation doivent avoir un propriétaire et
  une procédure documentés.
- Traiter explicitement les erreurs des dépendances externes, les délais d’attente et les
  indisponibilités. Les répétitions sont bornées et réservées aux opérations sûres à répéter.
- Définir avant production les objectifs de disponibilité, de perte de données et de reprise
  (RPO/RTO), ainsi que la stratégie de sauvegarde et des tests de restauration.
- Les exigences précises RGPD, consentement, export et suppression des données, audit et réponse
  aux incidents restent à formaliser dans les documents de sécurité et d’exploitation.

## Gestion de la configuration

- Séparer la configuration non secrète des secrets. Les valeurs propres à un environnement ne
  sont pas codées en dur dans la logique métier ou les clients.
- La configuration serveur est fournie à l’exécution par l’environnement de déploiement ou un
  gestionnaire de secrets approuvé. Les secrets ne sont ni versionnés, ni inclus dans les images,
  journaux, bundles web/mobile ou rapports de CI.
- Valider au démarrage les variables obligatoires, leur type, format et contraintes ; faire
  échouer le démarrage avec un message indiquant la clé/configuration manquante sans imprimer sa
  valeur secrète.
- Les valeurs par défaut ne sont acceptables que pour des paramètres non sensibles dont le
  défaut est sûr dans tous les environnements concernés. Ne pas fournir de fallback silencieux
  pour les secrets, clés, URL de base de données ou mécanismes de sécurité.
- Les clients ne reçoivent que des valeurs explicitement publiques. Toute variable incorporée
  dans un bundle client est considérée publique, même si son nom suggère le contraire.
- Documenter les clés de configuration, leur portée et leur caractère obligatoire sans inscrire
  de valeurs secrètes. Fournir un fichier d’exemple sans secret lorsque les manifestes seront
  créés.
- Les workflows GitHub Actions utilisent des permissions minimales et des secrets d’environnement
  limités au job qui en a besoin. Les secrets ne sont pas transmis aux workflows de contributions
  non fiables.
- Les noms de variables, la structure des fichiers d’environnement, les gestionnaires de
  secrets et les mécanismes de rotation restent à définir avec l’hébergement.

## Qualité et évolutivité

- Préserver la parité des parcours métier web/mobile du MVP tout en testant séparément les
  comportements dépendants de la plateforme.
- Évaluer les performances sur des scénarios, jeux de données et volumes représentatifs. Les
  objectifs de latence mentionnés dans les documents produit doivent être mesurés ; ne pas
  ajouter un cache ou un moteur spécialisé avant qu’un benchmark identifie un besoin.
- Tester les règles métier au niveau unitaire, les frontières API et données au niveau
  intégration, et les parcours critiques web avec Playwright. Ajouter des tests sur appareils
  réels lorsque les capacités natives le nécessitent.
- Toute modification d’architecture doit préserver les contrôles d’accès, la confidentialité,
  la possibilité de migration des données et la cohérence des contrats clients/API.
- Les vérifications automatisées et les déploiements sont orchestrés par GitHub Actions ; les
  environnements d’exécution et les services de production restent hébergés séparément.

## Décisions d’architecture

- Une décision qui modifie les frontières de composants, les technologies autorisées, les
  contrats de données, la sécurité, le coût d’exploitation ou les possibilités de migration doit
  être consignée comme ADR dans `decisions/`.
- Une ADR est requise notamment pour : ajouter/remplacer une technologie ou un fournisseur de
  production ; changer les frontières ou le sens des dépendances ; introduire un service,
  stockage, base, file, cache ou traitement asynchrone ; modifier le modèle d’identité, les rôles,
  les permissions ou le partage ; décider du contrat API/versionnement ; changer la résidence,
  la rétention, le chiffrement ou le cycle de vie des données ; modifier le mode de stockage ou
  de transfert des médias ; ajouter une dépendance qui traite des données personnelles ou des
  secrets ; accepter un coût récurrent ou un verrouillage fournisseur significatif ; déroger à
  une règle d’architecture.
- Une correction locale qui respecte une décision acceptée et ne change ni contrat ni frontière
  n’exige pas d’ADR. Si l’applicabilité de cette règle est incertaine, demander une revue
  technique avant de fusionner.
- Un ADR présente le contexte, la décision, les options envisagées, les conséquences, les risques
  et le statut (proposé, accepté, remplacé ou rejeté).
- Une décision ouverte ne devient pas un choix implicite par simple usage dans le code. En
  attendant sa validation, ne pas introduire la dépendance correspondante en production.
- Lorsqu’une décision acceptée change, mettre à jour ce document, la pile technique, les ADR et
  les configurations ou contrats affectés dans le même changement lorsque c’est possible.

## Points restant à décider

- Contrat API : style, versionnement, enveloppe d’erreur, authentification et documentation.
- Modèle relationnel détaillé : propriétaire des recettes, rôles, partage, variantes, historique
  et suppression.
- Fournisseurs et protocoles pour l’authentification, les courriels, l’OCR et les notifications.
- Traitement et structuration OCR, stratégie de correction et seuils de confiance.
- Stockage objet concret, transfert direct ou via API, quotas, validation et cycle de vie.
- Synchronisation hors ligne, données mises en cache et résolution des conflits.
- Hébergement, environnements, observabilité, objectifs de disponibilité, sauvegardes et reprise.
- Politique de conservation, export et suppression des données, ainsi que contrôles RGPD détaillés.
