# Conventions de développement — Bon App’

Ces conventions s’appliquent aux applications et paquets du monorepo. Elles complètent la
[pile technique](./technology-stack.md) sans remplacer les décisions d’architecture ni les
configurations d’outillage. Les règles décrites ici devront être automatisées par la
configuration du dépôt lorsque les manifestes seront créés.

## Principes généraux

- Privilégier un code lisible, explicite et typé ; choisir la solution la plus simple qui
  respecte les besoins établis.
- Garder chaque changement ciblé et cohérent. Éviter la duplication de logique métier entre
  web, mobile et API lorsqu’un paquet partagé est approprié.
- Ne pas ajouter de dépendance, service externe ou abstraction sans besoin identifié et décision
  compatible avec la pile technique.
- Documenter les décisions structurantes dans `decisions/` et les contrats ou comportements
  durables dans `architecture/`.
- Ne pas masquer les erreurs : les traiter au niveau qui peut fournir une action utile, les
  signaler clairement et conserver un contexte de diagnostic sans exposer de données sensibles.

## TypeScript et format

- Utiliser TypeScript pour le code applicatif. Activer le mode strict et corriger les erreurs de
  types plutôt que de les contourner.
- Éviter `any`. Pour les valeurs externes ou inconnues, utiliser `unknown`, valider leur forme,
  puis les convertir vers un type métier explicite.
- Typer les entrées et sorties des fonctions aux frontières des modules, ainsi que les contrats
  échangés entre applications et API.
- Utiliser deux espaces d’indentation, des points-virgules, des chaînes entre apostrophes, des
  virgules finales dans les constructions multilignes et une largeur de ligne cible de
  100 caractères.
- Enregistrer les fichiers texte en UTF-8, avec fins de ligne LF et sans espaces en fin de ligne.
- Formater automatiquement plutôt que corriger manuellement les écarts. La configuration
  centralisée du formateur et du linter, leurs versions et les scripts à exécuter restent à
  ajouter au monorepo ; aucun sous-projet ne doit définir des règles divergentes.
- Les fichiers de code et de test utilisent l’extension `.ts` ou `.tsx` selon qu’ils contiennent
  du JSX. Utiliser `import type` pour les imports uniquement utilisés comme types.
- Regrouper les imports dans cet ordre, avec une ligne vide entre groupes : modules natifs Node,
  dépendances externes, alias internes, puis chemins relatifs. Supprimer les imports inutilisés.
- N’ajouter un commentaire que pour expliquer une contrainte ou une décision qui ne ressort pas
  clairement du code. Préférer améliorer le nom ou la structure quand cela suffit.

## Nommage et organisation

- Utiliser `camelCase` pour les variables, fonctions, méthodes, propriétés et paramètres ;
  `PascalCase` pour les classes, types, interfaces, composants React et enums.
- Réserver `UPPER_SNAKE_CASE` aux constantes globales partagées qui représentent une valeur fixe.
  Les variables locales déclarées avec `const` restent en `camelCase`.
- Écrire les identifiants, noms de fichiers et messages d’erreur techniques en anglais ; les
  libellés présentés aux utilisateurs doivent passer par le mécanisme de localisation retenu,
  sans texte d’interface codé en dur.
- Préfixer les hooks React par `use`. Nommer les booléens avec une forme affirmative qui indique
  leur sens (`isLoading`, `hasAccess`).
- Nommer les composants React `PascalCase.tsx`. Nommer les modules, fonctions, services et tests
  en `kebab-case.ts` avec un suffixe `.test.ts` ou `.test.tsx`. Les conventions de fichiers
  imposées par NestJS (par exemple `recipes.service.ts`) et Expo Router priment sur cette règle ;
  les tests restent suffixés `.test.ts`.
- Nommer les types et interfaces selon le concept métier, sans préfixes `I` ou suffixes
  redondants comme `Type` ; suffixer explicitement les DTO par `Dto` lorsque cela les distingue
  des modèles métier.
- Organiser le code par fonctionnalité ou domaine métier, et non en répertoires globaux
  `utils/`, `services/` ou `components/` sans limite de domaine. Exemple de forme cible :

  ```text
  apps/api/src/recipes/
    recipes.module.ts
    recipes.controller.ts
    recipes.service.ts
    recipes.service.test.ts
  apps/mobile/app/recipes/
    index.tsx
  packages/recipes/src/
    normalize-recipe-title.ts
    normalize-recipe-title.test.ts
  ```

- Placer dans `packages/` uniquement le code réellement partagé et indépendant des détails
  propres à une application. Garder les intégrations de plateforme dans `apps/`.
- Garder les tests unitaires à proximité du module testé ; placer les parcours de bout en bout
  dans `tests/e2e/`. Éviter les fichiers « fourre-tout » et les modules dont les responsabilités
  n’ont pas de lien cohérent.

## Commentaires et documentation du code

- Écrire les commentaires en anglais, comme le code. Expliquer pourquoi une décision ou une
  contrainte existe, pas répéter l’instruction immédiatement lisible.
- Ajouter un commentaire pour une contrainte de sécurité, un contournement temporaire ou une
  règle métier non évidente ; référencer l’ADR ou l’issue quand elle existe.
- Ajouter un TODO uniquement s’il est lié à une issue suivie, par exemple `TODO(#123): ...`.
  Ne pas laisser de TODO sans responsable ou suivi.
- Documenter les fonctions exportées d’un paquet partagé lorsque leur contrat, les erreurs
  possibles ou les limites d’usage ne sont pas évidents à partir des types et des noms.
- Garder la documentation utilisateur, les décisions et les explications d’architecture dans
  les fichiers Markdown pertinents plutôt qu’en commentaires de code.

## Dépendances soumises à validation

Toute nouvelle dépendance directe doit être justifiée dans la pull request. Avant son ajout,
vérifier qu’elle n’est pas déjà couverte par la plateforme ou une dépendance approuvée, qu’elle
est maintenue, compatible avec Expo SDK et Node.js retenus, acceptable en licence et en sécurité,
et que son coût, ses données traitées et son impact de taille/exécution sont connus. Verrouiller
la version dans le manifeste et le lockfile.

Sans décision documentée dans un ADR et validation de la revue technique, ne pas ajouter :

- un fournisseur ou SDK de production pour l’authentification, les courriels, l’OCR, le stockage
  média, les notifications, l’analytique ou tout autre service externe encore ouvert dans la
  pile technique ;
- une bibliothèque cryptographique, d’authentification, de gestion de secrets ou de permissions
  qui remplace ou complète les mécanismes retenus ;
- un ORM, un outil de migration ou une autre base de données avant décision d’architecture ;
- un framework UI, un routeur, un gestionnaire d’état, un client HTTP ou un système de validation
  redondant avec une solution déjà retenue ou fournie par la plateforme ;
- une dépendance native ou un script d’installation ayant accès au système, au réseau ou aux
  secrets sans revue de sécurité et validation de compatibilité ;
- une dépendance non maintenue, sans licence claire, avec vulnérabilité connue non traitée,
  ou ajoutée depuis une URL mutable sans version verrouillée.

Une dépendance de développement, de test ou de build est également une dépendance et suit ces
règles. Les outils prévus par la pile technique ne sont pas automatiquement installés : leurs
versions doivent être verrouillées et leur compatibilité confirmée.

## Applications Expo et React

- Favoriser les composants fonctionnels petits et focalisés ; séparer affichage, état d’écran et
  logique métier lorsque cela améliore la compréhension ou les tests.
- Utiliser les API multiplateformes d’Expo/React Native pour les parcours partagés. Isoler les
  comportements web, iOS ou Android derrière des modules ou composants spécifiques plutôt que
  multiplier les conditions de plateforme dans la logique métier.
- Garder la logique métier indépendante de l’interface et testable sans rendu de composant.
- Prévoir les états de chargement, vide, réussite et erreur des interactions asynchrones. Ne pas
  présenter une opération comme réussie avant confirmation.
- Respecter l’accessibilité : libellés compréhensibles, navigation adaptée, retours d’état et
  contrôles utilisables au clavier ou avec les technologies d’assistance lorsque la plateforme
  le permet.
- Ne pas stocker de secret dans l’application cliente ; tout ce qui est livré au navigateur ou
  à l’application mobile doit être considéré comme public.

## API NestJS et données

- Regrouper les fonctions de l’API par domaine métier et garder une séparation claire entre
  contrôleurs, règles métier et accès aux données.
- Valider les données aux frontières de confiance. Ne pas considérer les types TypeScript comme
  une validation des requêtes reçues à l’exécution.
- Appliquer les permissions côté serveur à chaque opération portant sur un utilisateur, une
  recette ou un espace familial ; ne jamais se fier uniquement à l’état ou aux contrôles client.
- Retourner des erreurs explicites et cohérentes sans révéler de détails internes, secrets ou
  données d’un autre utilisateur. Journaliser les informations utiles au diagnostic avec
  minimisation des données personnelles.
- Utiliser des requêtes paramétrées. Encadrer les opérations multi-étapes qui doivent rester
  cohérentes dans une transaction.
- Versionner les évolutions de schéma par des migrations révisables ; ne pas modifier la base
  de production manuellement sans procédure documentée.
- Conserver les médias dans le stockage objet privé compatible S3 et leurs métadonnées dans
  PostgreSQL. Vérifier les droits côté API avant de délivrer ou d’utiliser un accès temporaire.

## Erreurs, sécurité et configuration

- Ne jamais committer de mot de passe, jeton, clé privée ou secret de service. Utiliser les
  mécanismes de configuration et de secrets des environnements concernés.
- Valider les variables de configuration au démarrage et échouer explicitement si une valeur
  obligatoire manque ou est invalide.
- Valider les données externes à leur frontière d’entrée ; les types TypeScript seuls ne valident
  pas les données reçues à l’exécution.
- Intercepter une erreur uniquement pour ajouter du contexte utile, la convertir vers une erreur
  métier/API, appliquer une récupération prévue ou la traiter. Sinon, la propager. Ne jamais
  transformer un échec en valeur de succès par défaut.
- Dans un `catch`, considérer la valeur comme `unknown` et vérifier son type avant d’en lire les
  propriétés. Ne pas exposer les détails internes de l’erreur à l’utilisateur.
- Les erreurs présentées au client doivent indiquer une action ou un résultat compréhensible ;
  elles ne doivent contenir ni stack trace, ni requête, ni secret, ni détail d’un autre compte.
- Ne réessayer que les erreurs transitoires, avec un nombre de tentatives et un délai bornés ;
  vérifier que l’opération peut être répétée sans effets indésirables.
- Protéger les données personnelles dans les logs, rapports de test, captures et messages
  d’erreur. Ne pas enregistrer le contenu privé des recettes ou des médias sans justification.
- Appliquer le principe du moindre privilège aux accès applicatifs et aux workflows CI.

## Journalisation

- Utiliser le logger du framework ou un logger structuré approuvé ; ne pas utiliser `console.log`
  dans le code applicatif. Les tests peuvent espionner un logger ou utiliser un faux logger.
- Enregistrer les événements opérationnels utiles avec un niveau approprié : `error` pour un
  échec nécessitant investigation, `warn` pour une situation anormale récupérée, `info` pour un
  événement opérationnel important et `debug` pour le diagnostic temporaire.
- Ajouter un identifiant de corrélation ou de requête lorsqu’il est disponible, ainsi que le
  nom du module ou de l’opération. Ne jamais journaliser mots de passe, jetons, clés, contenu de
  recette, image, message privé ou autres données personnelles non nécessaires.
- Journaliser une erreur une seule fois au niveau qui la traite définitivement ; éviter les
  doublons à chaque couche. Conserver la classe d’erreur et la stack uniquement dans les logs
  serveur protégés, jamais dans la réponse client.
- Ne pas ajouter de suivi d’accès sensible ou de données d’audit sans définir les événements,
  la durée de conservation et les accès autorisés.

## Tests

- Écrire des tests Jest pour chaque règle métier non triviale et chaque branche d’erreur
  pertinente. Tester les résultats et effets observables plutôt que les détails internes.
- Pour chaque fonction pure, couvrir au minimum un cas nominal et les limites ou entrées invalides
  qui changent son comportement. Pour les opérations protégées, tester les refus d’accès autant
  que les accès autorisés.
- Utiliser des tests d’intégration pour vérifier les frontières importantes de l’API, la
  validation des requêtes, les permissions et les interactions avec la base de données.
- Utiliser Playwright pour les parcours web critiques : connexion, création/consultation de
  recette, recherche, partage et import lorsque ces parcours sont implémentés.
- Ajouter un test de régression pour tout bug corrigé lorsque cela est possible. Éviter les
  snapshots volumineux ou fragiles ; préférer des assertions ciblées.
- Garder les tests déterministes : pas de dépendance implicite à des services externes, à
  l’horloge ou à des données partagées. Utiliser des données fictives et non sensibles.
- Les scripts exacts de test, lint, vérification de types et build seront définis dans les
  manifestes puis exécutés par GitHub Actions avant fusion.

## Exemples de référence

### Exemple conforme 1 — fonction métier

```ts
export function normalizeRecipeTitle(title: string): string {
  const normalizedTitle = title.trim().replace(/\s+/g, ' ');

  if (normalizedTitle.length === 0) {
    throw new RangeError('Recipe title must not be empty.');
  }

  return normalizedTitle;
}
```

Cette fonction a un nom explicite, un type de retour, aucun effet caché et rejette explicitement
une entrée vide après normalisation.

### Exemple conforme 2 — test du comportement et de l’erreur

```ts
import { describe, expect, it } from '@jest/globals';
import { normalizeRecipeTitle } from './normalize-recipe-title';

describe('normalizeRecipeTitle', () => {
  it('trims and collapses whitespace', () => {
    expect(normalizeRecipeTitle('  Tarte   aux pommes \n')).toBe('Tarte aux pommes');
  });

  it('rejects a title that is empty after trimming', () => {
    expect(() => normalizeRecipeTitle(' \n\t ')).toThrow(RangeError);
  });
});
```

Le test couvre le cas nominal et l’entrée invalide sans dépendre d’un service externe. L’import
`@jest/globals` suppose que cette forme est retenue lors de la configuration de Jest ; elle devra
être adaptée si le dépôt choisit une configuration globale Jest sans imports explicites. Dans le
code, la fonction et son test seraient placés dans des fichiers voisins nommés
`normalize-recipe-title.ts` et `normalize-recipe-title.test.ts`.

### Contre-exemple — à ne pas reproduire

```ts
export function normalize_title(title: any) {
  try {
    console.log(title);
    return title.trim() || 'Recipe';
  } catch {
    return 'Recipe';
  }
}
```

Ce code mélange des conventions de nommage, désactive le typage, journalise potentiellement un
contenu privé, masque l’erreur et transforme une entrée invalide en réussite apparente.

## Règles à préciser avant automatisation

- Choisir et configurer le formateur et le linter, leurs versions, les règles exactes d’import et
  les commandes CI. Les règles de format ci-dessus sont normatives, mais pas encore vérifiées
  automatiquement.
- Confirmer l’alias des imports, les règles d’export des modules, les suffixes des DTO, les
  limites de taille des fichiers, le mécanisme de localisation et la convention de nommage des
  migrations.
- Définir le schéma d’erreurs API (codes, forme JSON et correspondance des erreurs métier vers
  les statuts HTTP) et les règles de retry propres aux appels réseau.
- Choisir/configurer le logger structuré, les champs autorisés, les niveaux par environnement,
  la politique de rétention et les exigences d’audit.
- Verrouiller la configuration Jest (globals ou imports explicites, sélection des tests et
  setup), l’environnement d’intégration de la base, ainsi que les navigateurs et seuils CI des
  tests Playwright.
- Définir qui peut approuver les exceptions aux dépendances interdites et où consigner leur
  validation. D’ici là, une décision documentée dans un ADR et une revue technique sont requises.

## Revue et livraison

- Proposer les changements par pull request, avec un objectif clair, un résumé des effets
  visibles et les validations réalisées.
- Garder les pull requests assez ciblées pour permettre une revue efficace. Signaler les
  migrations, changements de configuration et impacts de sécurité.
- Ne fusionner qu’après revue et réussite des vérifications CI exigées par les règles du dépôt.
- Mettre à jour la documentation directement liée au comportement ou à la configuration
  modifiés.
