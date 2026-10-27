# Pile technique — Bon App’

> **Périmètre de référence :** MVP web, mobile iOS/Android et API. L’application web et les
> applications mobiles partagent autant que possible le même code et les mêmes fonctionnalités
> métier.

## Principes de choix

- Privilégier les solutions gratuites ou libres lorsqu’elles répondent aux besoins.
- Réutiliser TypeScript et les écrans partagés sur web et mobile afin de limiter le nombre de
  langages et de maintenir une expérience cohérente.
- Favoriser une architecture et des technologies permettant de déployer facilement
  l’application dans différents clouds, sans dépendance inutile à un fournisseur ; éviter
  toutefois la complexité de solutions de portabilité qui ne répondent pas à un besoin établi.
- Choisir des versions maintenues et compatibles entre elles ; verrouiller les versions
  effectivement installées dans le dépôt avant le développement.
- Ne pas considérer les services payants ou les intégrations de phases ultérieures comme
  autorisés tant qu’un responsable et un budget ne sont pas définis.

## Technologies retenues pour le MVP

| Domaine | Choix et version cible | Rôle | Justification | Alternatives écartées |
|---|---|---|---|---|
| Langage applicatif | TypeScript, version compatible avec Expo SDK 58 et NestJS 11 ; version exacte à verrouiller dans le manifeste | Applications web et mobiles, API et contrats partagés | Typage statique et langage commun aux couches JavaScript ; réduit les divergences de modèles entre client et serveur | JavaScript seul, car il ne fournit pas les contrôles de types à la compilation ; Dart/Flutter, car il imposerait un second langage et une pile séparée |
| Runtime serveur | Node.js 24 LTS, dernier correctif de la branche 24 | Exécution de l’API | Branche LTS adaptée à la production et compatible avec l’écosystème TypeScript retenu | Node.js « Current » 26, pour éviter de baser le MVP sur une branche non-LTS ; versions EOL, non maintenues |
| Framework API | NestJS 11.x, dernier correctif compatible avec Node.js 24 | API backend : recettes, comptes, espaces, rôles, partage et recherche | Framework TypeScript modulaire adapté au backend structuré décrit dans la spécification | Express seul, moins structurant pour les modules et responsabilités du produit ; framework dans un autre langage, qui introduirait une deuxième pile |
| Application web et mobile | Expo SDK 58, incluant React Native 0.88 ; cible web via React Native Web et React DOM aux versions compatibles résolues par le SDK | Application web dans le navigateur et applications iOS/Android ; partage des écrans, composants et logique métier | Une seule application Expo réduit les divergences et permet de conserver la même expérience fonctionnelle sur les trois plateformes. React Native Web rend les composants partagés dans le navigateur | Application web React séparée, qui dupliquerait écrans et logique sans besoin web distinct établi ; Swift/Kotlin ou Flutter, qui ajouteraient une pile séparée |
| Navigation multiplateforme | Expo Router fourni avec Expo SDK 58 ; version compatible résolue par le SDK | Navigation et liens profonds sur web, iOS et Android | Une seule définition des routes et des liens profonds pour les trois plateformes | Ajouter un routeur spécifique au web ou au mobile, qui dupliquerait la configuration |
| Base de données | PostgreSQL 18, dernier correctif de la branche 18 | Données relationnelles : utilisateurs, recettes, ingrédients, variantes, espaces, rôles et métadonnées | Modèle relationnel adapté aux liens et permissions ; logiciel libre, sans licence par utilisateur | MongoDB, moins naturel pour les relations et contraintes d’intégrité centrales ; base propriétaire payante, inutile à ce stade |
| Gestion des dépendances | pnpm 12.x, correctif exact verrouillé dans `packageManager` | Installation reproductible et gestion des espaces de travail `apps/` et `packages/` | Répond à la structure de dépôt en monorepo et évite de dupliquer les dépendances | npm, qui conviendrait également, mais apporte moins de bénéfice ici pour la gestion d’un monorepo ; Yarn, écarté pour éviter un second gestionnaire |
| Hébergement du code et CI | GitHub ; GitHub Actions pour les workflows automatisés | Dépôt, revue des changements, suivi des tâches et vérifications à chaque pull request | Centralise la collaboration et permet d’exécuter les scripts existants du projet sans remplacer l’hébergement applicatif ; quotas et fonctionnalités de sécurité à vérifier selon le forfait | Une plateforme Git distincte ajouterait un outil de collaboration et de CI sans besoin établi |
| Tests API | Jest 30.x, version exacte verrouillée | Tests unitaires et d’intégration de l’API | Écosystème mature et prise en charge par l’outillage NestJS | Mocha/Chai, qui nécessiterait davantage d’assemblage ; plusieurs runners de tests dans la même API |
| Tests mobile | Jest 30.x avec `jest-expo` compatible avec SDK 58, plus React Native Testing Library compatible | Tests unitaires et de composants de l’application | Permet de tester les composants et comportements mobiles dans la pile Jest retenue | Tests exclusivement manuels, insuffisants pour prévenir les régressions ; un deuxième runner sans besoin établi |
| Tests navigateur | Playwright 1.x, version exacte verrouillée | Tests de bout en bout dans les navigateurs de bureau et mobiles pour connexion, recettes, recherche, partage et parcours d’import | Un navigateur réel est nécessaire pour valider navigation, rendu responsive et interactions web ; Jest seul ne valide pas ces comportements de bout en bout | Tests manuels uniquement, répétables mais coûteux et non adaptés à la non-régression ; tests Jest seuls, qui ne couvrent pas les intégrations réelles du navigateur |
| Build web | Expo CLI compatible avec SDK 58 ; export web via `expo export --platform web` | Production des fichiers web distribuables | Réutilise le pipeline Expo et produit un export web sans ajouter de framework ni de bundler ; le service d’hébergement reste à choisir | Next.js ou un bundler séparé, non justifiés sans besoin de rendu serveur ou de référencement public |
| Build mobile | Expo Application Services (EAS Build), CLI compatible avec SDK 58 ; version de CLI à verrouiller | Génération des builds iOS et Android | Chemin de build Expo intégré, sans maintenir deux pipelines natifs au démarrage ; vérifier que les quotas gratuits suffisent | Builds natifs locaux, sans coût de service mais avec plus de configuration et de maintenance ; Expo Go seul, qui ne produit pas les livrables de distribution |
| Build API | TypeScript (`tsc`) via les scripts NestJS ; versions définies par le lockfile | Vérification des types et compilation serveur | Outil du langage déjà retenu, sans bundler serveur supplémentaire requis par le besoin décrit | Ajouter un bundler avant qu’un besoin de performance ou de packaging soit démontré |

La cible web est une application métier responsive, accessible après connexion, et non un site
marketing ou un site public indexable. Elle doit couvrir les mêmes parcours métier MVP que le
mobile ; les capacités propres à l’appareil (caméra, import depuis une messagerie, partage
système et notifications) utilisent les mécanismes du navigateur ou un parcours de repli. Aucun
rendu serveur ni framework de référencement n’est retenu en l’absence de besoin public.

## Rôle de GitHub

GitHub est retenu pour héberger le code source et organiser la collaboration : pull requests,
revues de code, Issues et Projects pour le suivi du travail. Les changements proposés devront
passer par une pull request ; les vérifications CI requises avant fusion seront définies dans
les règles de protection de branche.

GitHub Actions exécutera les commandes du dépôt sur les pull requests et les mises à jour de la
branche principale : installation reproductible avec pnpm et lockfile, vérification des types,
tests Jest, build de l’API et de l’application, puis tests Playwright lorsqu’un environnement web
de test est disponible. Les builds et déploiements vers les hébergeurs web ou API pourront être
déclenchés par Actions, mais nécessiteront un hébergeur et des secrets d’accès distincts. EAS
Build demeure la solution retenue pour produire les builds mobiles ; Actions peut l’orchestrer,
sans remplacer EAS ni les comptes Apple et Google.

Dependabot pourra proposer les mises à jour de dépendances et signaler les vulnérabilités
connues. L’analyse de code et la détection de secrets pourront être activées si elles sont
disponibles dans le forfait et la configuration du dépôt. Les workflows devront limiter leurs
permissions et ne pas exposer de secrets aux contributions non fiables. Les quotas, coûts et
fonctionnalités disponibles dépendent du forfait GitHub et de l’usage.

GitHub ne sert pas de backend Bon App’ : il n’héberge ni l’API de production, ni PostgreSQL, ni
les photos et autres médias des utilisateurs, et ne fournit pas l’authentification produit ou
l’OCR. GitHub Pages n’est pas retenu pour l’application métier connectée.

Les numéros de versions majeures constituent le socle de compatibilité. Les versions exactes
des paquets JavaScript devront être fixées dans `package.json` et le lockfile ; les correctifs
de sécurité devront être mis à jour sans changer de majeure sans revue de compatibilité.
Expo impose de choisir les versions de ses bibliothèques natives à partir de son catalogue
SDK, plutôt que de fixer indépendamment des versions arbitraires.

## Services et composants dont le choix reste ouvert

Ces éléments répondent à des responsabilités identifiées dans la spécification, mais celle-ci
ne donne pas assez d’informations pour autoriser honnêtement un fournisseur ou une version.
Ils ne doivent pas être intégrés avant les décisions et contrôles indiqués ci-dessous.

| Responsabilité | Proposition ou options à évaluer | Rôle | Justification / alternatives | État et décision manquante |
|---|---|---|---|---|
| OCR | Comparer un OCR local gratuit avec Google Cloud Vision et AWS Textract, explicitement cités dans la spécification | Reconnaître le texte des photos de recettes | Le traitement local peut limiter les coûts et l’envoi de données ; les services cloud peuvent offrir un OCR plus robuste, mais impliquent coûts, transfert de données et dépendance fournisseur | **Non autorisé à ce stade.** Mesurer qualité et latence sur un corpus représentatif, notamment contre la cible de moins de 5 secondes ; définir consentement, région de traitement et budget. La spécification ne tranche pas |
| Compréhension et structuration du texte | À concevoir après évaluation OCR | Transformer le texte reconnu en ingrédients, quantités, unités et étapes, avec correction utilisateur | L’OCR extrait du texte ; la reconnaissance de sections et l’interprétation des recettes sont une responsabilité distincte | **Manquant.** Aucun moteur, règles, modèle, seuil de confiance ni comportement de correction n’est spécifié |
| Nettoyage d’image | Pipeline à définir et à benchmarker sur appareils cibles | Recadrage, perspective, contraste et suppression d’ombres | La spécification demande ces fonctions, mais ne prescrit aucune bibliothèque ou exécution côté serveur/appareil | **Manquant.** Choisir l’emplacement du traitement, les opérations MVP, leur coût et leur latence |
| Stockage des médias | Stockage objet compatible avec l’API S3 ; fournisseur à sélectionner | Photos, vidéos et notes vocales, avec métadonnées conservées dans PostgreSQL | Sépare les fichiers volumineux des données relationnelles et permet de choisir entre plusieurs fournisseurs compatibles ; l’API S3 ne garantit pas à elle seule une compatibilité identique de toutes les fonctions | **Choix retenu pour le MVP : stockage objet compatible S3.** Sélectionner le fournisseur, vérifier les opérations S3 nécessaires et comparer quotas, région, chiffrement, sauvegardes, rétention et coûts. Les objets doivent rester privés ; définir le contrôle d’accès via l’API et le mécanisme de transfert sécurisé |
| Notifications push | Apple Push Notification service (APNs) et Firebase Cloud Messaging (FCM), via l’intégration compatible Expo | Notifications de commentaires, variantes et activités | Les notifications natives iOS/Android nécessitent leurs canaux de distribution ; il faut éviter une solution tierce payante tant que les besoins restent standards | **À confirmer.** Choisir l’acheminement Expo ou direct, les identifiants de comptes et les règles de consentement. Une notification push n’équivaut pas à une synchronisation temps réel |
| Synchronisation et mode hors ligne | À concevoir dans l’application et l’API | Consultation hors ligne et synchronisation au retour réseau | La spécification en fait une exigence ; aucune technologie ni stratégie de résolution des conflits n’est donnée | **Manquant.** Définir stockage local, données disponibles hors ligne, conflits, suppressions et stratégie de reprise |
| Recherche | Recherche PostgreSQL à évaluer avant l’ajout d’un moteur spécialisé | Filtres par ingrédient, saison, temps, auteur, difficulté et variante | Commencer par la base retenue limite coût et exploitation ; un index dédié ne se justifiera que si la mesure montre que l’objectif de moins de 300 ms n’est pas atteint | **Choix provisoire : PostgreSQL.** Définir corpus, requêtes, pagination et charge de référence ; ne pas ajouter de moteur externe sans benchmark |
| Authentification et courriels | À décider ; aucun fournisseur retenu | Comptes, sessions, récupération et invitations | Ces fonctions sont nécessaires aux espaces familiaux et au partage, mais aucun service n’est cité dans la spécification | **Manquant.** Choisir auth interne ou fournisseur, MFA éventuelle, courriels transactionnels, région et coûts |
| Hébergement API et PostgreSQL | À décider ; privilégier un hébergement avec offre gratuite exploitable pour le prototype, puis comparer les coûts de production | Exécution, base, réseau, sauvegardes et environnements | PostgreSQL est libre, mais son exploitation, la disponibilité et les sauvegardes ne sont pas gratuites par défaut | **Manquant.** Fournisseur, régions, environnements, objectifs de disponibilité, RPO/RTO, observabilité et budget |
| Partage WhatsApp/SMS | À définir selon les mécanismes réellement disponibles sur iOS et Android | Import d’une photo ou d’un message | La spécification décrit l’import, mais ne précise ni API officielle, ni flux d’interopérabilité, ni limites des plateformes | **Manquant.** Définir le parcours d’import système et le format accepté ; ne pas présumer un accès direct aux messages privés |
| Impression | API de fournisseur d’impression à sélectionner pour une phase ultérieure | Génération, commande et suivi de livres imprimés | Le service n’est nécessaire que lorsque la fonctionnalité de livres devient prioritaire | **Hors MVP / non autorisé.** Fournisseur, pays, coûts, qualité, données transmises et support à choisir avant implémentation |
## Pile technique autorisée

Pour démarrer le MVP, la liste d’autorisation proposée est limitée à :

- TypeScript, Node.js 24 LTS et NestJS 11.x pour l’API ;
- Expo SDK 58 / React Native 0.88 pour les applications web, iOS et Android, avec React Native Web et React DOM aux versions prises en charge par le SDK ;
- Expo Router dans la version prise en charge par SDK 58 pour la navigation multiplateforme ;
- PostgreSQL 18 ;
- stockage objet privé compatible avec l’API S3 pour les médias ; fournisseur et client technique à sélectionner ;
- pnpm 12.x pour le monorepo ;
- Jest 30.x et les adaptateurs de test compatibles avec Expo SDK 58 ; Playwright 1.x pour les parcours de bout en bout dans les navigateurs ;
- Expo CLI pour l’export web et EAS Build pour les builds mobiles ; `tsc` pour compiler l’API.

Cette autorisation reste conditionnée à la validation des versions exactes et de la
compatibilité Expo au moment de créer les manifestes. Aucun fournisseur OCR, de stockage média,
d’authentification, d’hébergement ou d’impression n’est retenu par ce document. Pour le stockage
média, seul le choix d’un service compatible S3 est acté ; le fournisseur reste à sélectionner.
Le web est une cible de l’application Expo partagée, pas un framework web distinct.

## Dépendances, versions et responsabilités à compléter

Avant d’engager l’implémentation, consigner les décisions suivantes dans des ADR et les
traduire en manifestes, configurations et procédures :

1. **Responsables et livraison :** propriétaire technique, environnements dev/staging/prod,
   hébergement, configuration des workflows GitHub Actions, déploiement API, gestion des secrets,
   observabilité, sauvegardes et restauration. La spécification exige résilience et journalisation,
   sans service ni responsable désigné.
2. **Versions verrouillées :** version exacte de TypeScript, NestJS, Expo CLI/EAS CLI,
   React Native Web, React DOM, Jest, Playwright, `jest-expo`, React Native Testing Library,
   PostgreSQL et outils système ; fichier `.nvmrc`/équivalent, champ `packageManager`, lockfile
   et politique de mise à jour. Pour GitHub Actions, choisir les actions utilisées et référencer
   chacune par son SHA de commit complet, définir les labels de runners nécessaires et fixer
   explicitement les versions des outils installés par les workflows. Les images des runners
   hébergés par GitHub évoluant dans le temps, leur label seul ne garantit pas une image
   immuable. Configurer Dependabot pour proposer les mises à jour des actions, puis les valider
   par revue et CI.
3. **Prérequis plateformes :** versions minimales iOS et Android (« versions récentes » est trop
   vague), versions de Xcode, Android SDK, JDK et Gradle compatibles avec Expo SDK 58, comptes
   Apple/Google, signature et distribution ; navigateurs et versions minimales supportés,
   matrice de tests web desktop/mobile, déploiement de l’export web, domaine et configuration
   HTTPS. EAS peut simplifier les builds mobiles, mais ne supprime pas les exigences de comptes
   et de signature.
4. **Données et sécurité :** stratégie de migrations de base, ORM ou accès SQL, modèle de
   permissions, chiffrement et gestion des clés, politique de conservation/suppression,
   consentement, droits RGPD, journalisation des accès sensibles et procédure de violation.
5. **Médias et fonctionnement hors ligne :** sélectionner le fournisseur de stockage objet
   compatible S3 et son client, puis définir stockage local web/mobile, limites de taille,
   formats, antivirus/validation, sauvegardes, synchronisation et résolution des conflits.
   Définir les équivalents web des fonctions natives (sélection de fichiers, caméra, partage
   système et notifications) et les parcours de repli dans le navigateur.
6. **OCR et performance :** moteur retenu, traitement local ou cloud, qualité minimale,
   corpus de mesure, métrique de latence p95, traitement des erreurs et responsabilité de la
   structuration sémantique. Clarifier aussi la différence entre l’objectif OCR de moins de
   5 secondes et l’objectif de capture de bout en bout de moins de 10 secondes.
7. **Qualité et tests :** tests d’intégration API, tests sur appareils iOS/Android réels et
   navigateurs supportés, tests d’accessibilité clavier/lecteurs d’écran, tests utilisateurs
   par persona, seuils de couverture éventuels et tests de performance correspondant aux
   objectifs de moins de 2 secondes et moins de 300 ms. Les commandes et critères d’acceptation
   par plateforme, ainsi que les règles de fusion et la disponibilité d’appareils réels en CI,
   restent à définir.
8. **Parité fonctionnelle web/mobile :** confirmer que le web couvre les mêmes parcours métier
   du MVP. Définir les adaptations nécessaires pour caméra, import WhatsApp/SMS, notifications,
   partage natif, mode hors ligne et autres fonctions dépendant du système.
9. **Hébergement web :** choisir un hébergement des fichiers exportés, ses environnements,
   déploiements, noms de domaine, en-têtes de sécurité, politique de cache et quotas/coûts.
10. **Contrat API :** style (REST ou autre), format des échanges, stratégie de versionnement,
   documentation et validation des requêtes/réponses. NestJS fournit une base pour exposer
   une API, mais la spécification ne définit pas son contrat.

## Références

- [Document de spécification produit v2.1](../product/Document-de-spécifications-produit-v2.1.pptx) — architecture, performance, sécurité, RGPD, tests et intégrations.
- [Expo SDK 58 — notes de version](https://expo.dev/changelog/sdk-58) — SDK 58 et React Native 0.88.
- [Versions Node.js](https://nodejs.org/en/about/previous-releases) — statut LTS des branches.
- [Politique de versions PostgreSQL](https://www.postgresql.org/support/versioning/) — durée de support et recommandation de correctifs à jour.
- [Installation pnpm](https://pnpm.io/installation) — ligne de version pnpm 12.
- [GitHub Actions](https://docs.github.com/actions) — automatisation des workflows de CI et de livraison.
- [Dependabot](https://docs.github.com/code-security/dependabot) — alertes de dépendances et mises à jour automatisées.
