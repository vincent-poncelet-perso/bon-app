# Definition of Done — Bon App’

Cette Definition of Done (DoD) décrit les critères minimaux pour considérer une fonctionnalité,
correction ou évolution technique terminée et fusionnable. Elle s’applique aux applications web
et mobiles, à l’API, aux packages partagés et à l’infrastructure du dépôt.

Une tâche n’est pas « done » si un critère applicable est en échec, non vérifié ou remplacé par
une supposition. Les critères non applicables doivent être indiqués avec une justification dans
la pull request.

## Critères d’acceptation

- Le changement répond au besoin et aux critères d’acceptation convenus avant son implémentation.
- Le comportement attendu et les états d’erreur sont décrits sans ambiguïté ; les cas limites
  pertinents sont identifiés.
- La fonctionnalité respecte les principes produit : préserver et transmettre les recettes,
  rester accessible et garder privées par défaut les recettes et les médias.
- Les impacts visibles par les utilisateurs sont cohérents entre web, iOS et Android, ou les
  différences de plateforme et leurs parcours de repli sont explicités.
- Aucun comportement hors périmètre ni changement fonctionnel non annoncé n’est inclus.

## Qualité de l’implémentation

- Le code suit les [conventions de développement](../architecture/coding-conventions.md) et les
  [règles d’architecture](../architecture/architecture-rules.md) : responsabilités claires,
  dépendances autorisées, types stricts et erreurs traitées explicitement.
- Le changement ne laisse pas de code mort, de TODO non suivi, de secret, de donnée réelle dans
  les tests ou de journalisation de données privées.
- Les nouvelles dépendances sont justifiées, compatibles, verrouillées et approuvées selon les
  règles de sécurité et d’architecture.
- Les changements de schéma de données utilisent une migration revue ; aucun changement manuel
  non documenté de la base n’est requis.
- Les erreurs ne sont pas masquées par une valeur de succès de substitution. Les messages
  présentés à l’utilisateur sont compréhensibles et ne révèlent pas les détails internes.

## Tests et vérifications

- Les tests unitaires couvrent la logique métier ajoutée ou modifiée, y compris les entrées
  invalides et erreurs pertinentes.
- Les tests d’intégration couvrent les frontières API, données, permissions ou fournisseurs
  touchées par le changement.
- Les parcours Playwright ou tests sur appareils réels sont ajoutés ou mis à jour lorsqu’un
  parcours utilisateur ou une capacité propre à la plateforme est concerné.
- Un test de régression est ajouté pour un bug corrigé lorsque cela est possible.
- Les vérifications disponibles et pertinentes passent : formatage, lint, vérification des
  types, tests ciblés, build et contrôles de sécurité CI.
- Les tests sont déterministes, utilisent des données fictives et ne dépendent pas implicitement
  d’un service externe.
- Toute vérification non exécutée ou impossible à automatiser est signalée dans la pull request
  avec sa raison et, si nécessaire, la validation manuelle de remplacement.

## Sécurité, confidentialité et accessibilité

- Les contrôles d’authentification et d’autorisation sont appliqués côté serveur à chaque
  ressource et action affectée ; les accès non autorisés échouent de manière sûre.
- Les entrées externes sont validées à l’exécution. Les limites de taille, types et valeurs
  autorisés sont appliqués selon le contrat concerné.
- Aucun secret, jeton, credential ou donnée confidentielle non autorisée n’est ajouté aux
  sources, bundles clients, logs, artefacts ou prompts.
- Les données personnelles sont minimisées ; les médias privés restent dans le stockage privé
  prévu et leurs accès temporaires respectent les règles de sécurité.
- Les erreurs et journaux ne divulguent ni secrets, ni contenu privé, ni détails d’un autre
  utilisateur.
- Les changements d’interface respectent les exigences d’accessibilité applicables : libellés,
  focus et navigation clavier, retours d’état et compatibilité avec les technologies
  d’assistance lorsque la plateforme le permet.
- Les nouvelles données, intégrations ou transferts vers un fournisseur disposent des décisions
  de sécurité et de confidentialité requises avant activation.

## Documentation et exploitation

- La documentation directement touchée est mise à jour : aide utilisateur, architecture,
  conventions, décisions, configuration ou procédures d’exploitation selon le changement.
- Les nouveaux paramètres de configuration sont documentés sans valeur secrète ; les valeurs
  obligatoires sont validées au démarrage et les valeurs publiques sont identifiées.
- Les changements nécessitant une ADR l’incluent ou référencent une ADR acceptée avant fusion.
- Les migrations, changements de permissions, impacts sur données existantes, sauvegardes,
  rétention et éventuels déploiements progressifs sont explicités dans la pull request.
- Les métriques ou procédures opérationnelles nécessaires à une nouvelle dépendance ou à un
  traitement critique sont définies avant mise en production.

## Revue et fusion

- La pull request décrit le problème, la solution, les effets visibles, les risques et les
  vérifications réalisées.
- Les changements restent ciblés et peuvent être relus ; les impacts de sécurité et les
  migrations sont mis en évidence.
- Une revue requise est approuvée et tous les contrôles CI obligatoires réussissent.
- Les vulnérabilités critiques ou élevées exploitables et les secrets confirmés bloquent la
  fusion, sauf exception formellement documentée, approuvée et assortie de mesures compensatoires
  et d’une échéance conformément aux règles de sécurité.
- La fonctionnalité est déployable sans étape manuelle non documentée. Si une configuration ou
  un service externe reste à fournir, la tâche est marquée bloquée ou la limitation est explicitée ;
  elle n’est pas déclarée prête pour la production.

## Checklist de pull request

### Contrôles obligatoires pour tout changement

```text
- [ ] Le besoin et les critères d’acceptation sont explicites ; le changement les satisfait.
- [ ] La pull request décrit le but, le comportement modifié, les risques et les validations.
- [ ] Un reviewer a approuvé le changement ; les commentaires bloquants sont résolus.
- [ ] Tous les contrôles CI requis pour le dépôt réussissent : format/lint, vérification des
      types, tests concernés, build et contrôles de sécurité configurés.
- [ ] Les tests couvrent les comportements modifiés, les erreurs pertinentes et les permissions
      concernées ; ils utilisent des données fictives et sont déterministes.
- [ ] Le code respecte les conventions, les règles d’architecture et les exigences de qualité ;
      aucune erreur n’est masquée et aucun TODO sans suivi n’est laissé.
- [ ] Aucun secret, donnée de production ou contenu confidentiel non autorisé n’est ajouté aux
      sources, prompts, journaux, captures ou artefacts.
- [ ] La documentation directement touchée, les paramètres de configuration et les ADR requises
      sont à jour ; les changements et limites connus sont signalés.
- [ ] Les contrôles conditionnels ci-dessous sont soit réalisés, soit marqués non applicables
      avec une justification dans la pull request.
```

### Contrôles selon le type de changement

```text
Produit et validation
- [ ] [Si comportement visible par l’utilisateur] Le Product Owner (PO) valide les critères
      d’acceptation sur une démonstration, un environnement de recette ou des preuves convenues.
- [ ] [Si différence web/mobile ou capacité plateforme] Les parcours concernés et les replis
      disponibles sont vérifiés sur les plateformes affectées.

Tests et qualité
- [ ] [Si API, persistance, permissions ou intégration fournisseur] Les tests d’intégration
      couvrent les frontières affectées, les cas négatifs et les échecs de dépendance.
- [ ] [Si parcours web ou interaction utilisateur critique] Les tests Playwright sont ajoutés
      ou exécutés.
- [ ] [Si fonctionnalité native, caméra, fichiers, partage ou notification] La validation sur
      appareil réel est effectuée lorsqu’une simulation ne suffit pas.
- [ ] [Si correction de bug] Un test de régression est ajouté, sauf impossibilité expliquée.

Sécurité et données
- [ ] [Si identité, permissions, partage ou ressource privée] Les tests couvrent accès autorisé,
      refusé, révocation et isolation entre utilisateurs/espaces.
- [ ] [Si fichier ou média] Format réel, taille, accès privé, expiration et suppression sont
      vérifiés selon les règles de sécurité applicables.
- [ ] [Si donnée personnelle, fournisseur externe ou prompt] Classification, minimisation,
      destination, consentement/autorisation et rétention sont validés ; l’ADR ou décision
      requise est acceptée avant activation.
- [ ] [Si changement de dépendance] Provenance, licence, vulnérabilités, compatibilité,
      dépendances transitives et lockfile sont revus.

Accessibilité
- [ ] [Si interface ou contenu utilisateur modifié] Libellés, ordre et visibilité du focus,
      navigation clavier, retours d’état et technologies d’assistance applicables sont vérifiés.
- [ ] [Si critère d’accessibilité non applicable] La raison liée à la nature du changement est
      indiquée dans la pull request.

Observabilité et exploitation
- [ ] [Si nouveau comportement serveur, intégration ou traitement asynchrone] Les erreurs
      pertinentes sont traçables sans données privées ; métriques, logs ou alertes nécessaires
      et propriétaires opérationnels sont identifiés.
- [ ] [Si migration, changement de configuration ou évolution exploitable] Procédure de
      déploiement, retour arrière ou reprise, impacts sur données et paramètres requis sont
      documentés.

Déploiement et validation en production
- [ ] [Si changement livré en production] Les prérequis, secrets/configurations, séquence de
      déploiement, stratégie de migration et conditions de retour arrière sont prêts.
- [ ] [Après déploiement en production] Les smoke tests et indicateurs convenus confirment le
      fonctionnement ; les erreurs ou régressions déclenchent la procédure de retour arrière ou
      d’incident.
- [ ] [Si le changement n’est pas destiné à être déployé immédiatement] Son statut et les
      dépendances ou validations restantes sont explicites ; il n’est pas présenté comme prêt
      pour la production.
```

La validation du PO porte sur les changements qui modifient un comportement produit visible ou
un critère d’acceptation. Pour un changement purement technique, de documentation ou de
maintenance sans impact produit visible, la revue technique tient lieu de validation. Les
contrôles conditionnels non applicables doivent être justifiés, pas simplement omis.

## Limites à compléter

Les scripts exacts, les plateformes et appareils de test requis, les seuils de couverture, les
budgets de performance, les niveaux d’accessibilité ciblés, les contrôles CI obligatoires, les
environnements de recette et les modalités de validation du PO seront fixés lorsque les
manifestes et workflows CI du MVP seront configurés. Tant qu’ils ne sont pas définis, aucune
valeur chiffrée implicite ne doit être considérée comme validée ; les vérifications manuelles
nécessaires doivent être consignées dans la pull request.
