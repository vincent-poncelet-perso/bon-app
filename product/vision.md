# Vision produit — Bon App’

*Vision synthétique fondée sur le [Document de spécification produit v2.1](./Document-de-spécifications-produit-v2.1.pptx).*

## Notre vision

**Faire de chaque recette un lien entre les générations.**

Bon App’ veut faire vivre le patrimoine culinaire familial. Une recette, c’est aussi les gestes appris, les variantes inventées et les souvenirs partagés autour d’elle. En réunissant ces traces, les familles peuvent transmettre non seulement ce que l’on cuisine, mais aussi les histoires et les savoir-faire qui donnent à chaque recette sa place dans leur mémoire.

## Le problème auquel nous répondons

Les recettes familiales sont dispersées entre carnets manuscrits, photos, messages et transmission orale. Elles deviennent difficiles à retrouver et à transmettre ; leurs variantes et les souvenirs qui les accompagnent risquent de se perdre. Les outils courants conservent des contenus, mais ne donnent pas aux familles un espace commun pour les organiser, les enrichir et les faire vivre.

## Pour qui

Bon App’ s’adresse aux familles et à leurs membres, notamment :

- aux aînés qui souhaitent transmettre leurs recettes et leur savoir-faire ;
- aux parents qui reçoivent des recettes par messagerie et veulent les retrouver facilement ;
- aux cuisiniers amateurs qui créent des recettes, les font évoluer et les partagent.

L’expérience doit rester simple et accessible à tous les âges, sans sacrifier la richesse des usages.

### Catégories d’usage — provisoires

Les documents suggèrent plusieurs pratiques qui peuvent se chevaucher : suivre une recette en cuisinant ; conserver et retrouver une recette pour la refaire ; recevoir des recettes par messagerie pour planifier ; préserver et transmettre des recettes manuscrites et leur histoire ; adapter et partager des recettes. Ces regroupements sont des pistes provisoires, étayées à des niveaux différents par un entretien et les usagers décrits dans la spécification ; les difficultés de recherche, de planification et de transmission restent souvent à vérifier. Voir [Catégories d’utilisateurs](./categories-utilisateurs.md).

## Notre promesse

Rassembler les recettes et les histoires qui les rendent uniques, pour que chaque génération puisse les retrouver, les transmettre et les faire siennes.

## Résultats attendus pour l’utilisateur

Ordre provisoire, fondé sur la force des éléments disponibles — pas sur une validation de priorité auprès d’un groupe d’utilisateurs :

- **En cuisinant, garder plus facilement le fil des étapes et avoir moins besoin de relire la recette pour retrouver où l’on en est.** Signal directement rapporté par U-001 ; à vérifier auprès d’autres personnes. Vérification : fréquence des épisodes de perte du fil suivis d’une relecture ; cible **à définir**. ([Irritants utilisateurs](./user-pain-points.md), IRR-003 ; [Catégories d’utilisateurs](./categories-utilisateurs.md))
- **En voulant refaire un plat, retrouver la recette choisie et les ajustements qui lui sont associés.** U-001 conserve certaines recettes et leurs ajustements dans Word pour les refaire, mais aucun échec de recherche n’est rapporté : **hypothèse à vérifier**. Vérification : la personne retrouve-t-elle la recette et l’ajustement recherché ? Cible **à définir**. ([Irritants utilisateurs](./user-pain-points.md), IRR-004 ; [Catégories d’utilisateurs](./categories-utilisateurs.md))
- **Dans une famille, pouvoir retrouver et transmettre les recettes importantes avec le savoir-faire ou les variantes qui leur sont associés.** Aligné sur l’ambition de la section [Notre vision](#notre-vision) ; U-001 juge fragile la transmission papier, sans incident rapporté : **hypothèse à vérifier**. Vérification : exemple concret de recette ou de savoir-faire effectivement transmis, manquant ou risquant de l’être. Cible **à définir**. ([Irritants utilisateurs](./user-pain-points.md), IRR-005 ; [Catégories d’utilisateurs](./categories-utilisateurs.md))

## Résultats attendus pour l’organisation

Ces résultats décrivent les changements recherchés pour la portée, la pérennité et la valeur du produit. Ils ne sont ni des bénéfices directs pour les utilisateurs ni des fonctionnalités à livrer.

Le registre des hypothèses à valider, distinguant les faits documentés des suppositions et couvrant désirabilité, faisabilité, viabilité, sécurité et exploitabilité, est disponible dans [le registre des hypothèses](./hypotheses.md).

### 1. Faire de Bon App’ l’espace où les recettes familiales sont effectivement centralisées

- **Résultat recherché :** augmenter la part des familles qui utilisent Bon App’ comme lieu durable pour enregistrer, retrouver et conserver leurs recettes, afin de réduire la dispersion décrite dans [Le problème auquel nous répondons](#le-problème-auquel-nous-répondons).
- **Indicateur :** proportion des familles actives ayant ajouté au moins une recette consultable dans leur espace commun, et nombre moyen de recettes conservées par famille active.
- **Méthode de mesure :** suivre les créations et consultations de recettes par famille dans les données produit, puis rapprocher ces usages d’une enquête ou d’entretiens permettant de confirmer que l’application remplace ou complète réellement les supports dispersés.
- **Valeur initiale :** à mesurer.
- **Cible :** à définir.
- **Échéance :** à définir.
- **Hypothèses à vérifier :**
  - les familles disposent bien de recettes dispersées qu’elles cherchent à rassembler ;
  - une famille comprenant plusieurs membres utilise le même espace comme référentiel ;
  - la centralisation est perçue comme durable plutôt que comme une simple duplication.

**Justification par la vision :** la promesse de « rassembler les recettes et les histoires » suppose un lieu commun durable. Le MVP doit donc donner aux familles un espace pour capturer, organiser et retrouver leurs recettes.

### 2. Faire circuler les recettes et le savoir-faire entre plusieurs générations

- **Résultat recherché :** augmenter la proportion des familles dans lesquelles une recette est partagée ou enrichie avec un membre d’une autre génération, afin de traduire la mémoire familiale en transmission effectivement réalisée.
- **Indicateur :** proportion des familles actives ayant au moins une recette partagée avec un membre d’une autre génération ou enrichie grâce à sa contribution.
- **Méthode de mesure :** analyser les invitations acceptées, les contributions et les modifications relatives à une recette, puis qualifier la relation générationnelle par un questionnaire familial ; compléter par des exemples qualitatifs de transmission.
- **Valeur initiale :** à mesurer.
- **Cible :** à définir.
- **Échéance :** à définir.
- **Hypothèses à vérifier :**
  - plusieurs générations ont suffisamment d’intérêt et d’accès pour participer ;
  - le partage entre générations est souhaité sans réduire le contrôle sur les recettes privées ;
  - une contribution identifiable constitue bien une transmission utile et non seulement une copie technique.

**Justification par la vision :** « Faire de chaque recette un lien entre les générations » est l’ambition centrale. La section sur les usages vise notamment les aînés transmetteurs, les parents et les cuisiniers amateurs, tandis que la promesse porte sur le partage de recette entre générations.

### 3. Accroître la richesse des mémoires familiales conservées dans Bon App’

- **Résultat recherché :** augmenter la part du patrimoine familial conservé avec ses gestes, variantes, anecdotes et médias, plutôt que comme une simple liste d’ingrédients ou une succession d’étapes.
- **Indicateur :** proportion des recettes familiales enrichies d’au moins un élément de mémoire : anecdote, photo, variante ou autre savoir-faire associé.
- **Méthode de mesure :** mesurer sur les fiches de recette la présence d’une anecdote, d’une photo, d’une variante ou d’un autre champ de savoir-faire ; échantillonner les fiches pour vérifier la qualité et la pertinence de l’enrichissement.
- **Valeur initiale :** à mesurer.
- **Cible :** au moins 25 % des recettes sont partagées ou enrichies, cible de travail déjà formulée dans la section [Comment mesurer les progrès du MVP](#comment-mesurer-les-progrès-du-mvp).
- **Échéance :** à définir.
- **Hypothèses à vérifier :**
  - les familles souhaitent conserver davantage que les seuls ingrédients et étapes ;
  - les éléments anecdotiques et les variantes peuvent être capturés sans rendre la saisie trop lourde ;
  - la présence d’un média ou d’une anecdote améliore réellement la mémorisation et la transmission.

**Justification par la vision :** Bon App’ veut préserver les gestes appris, les variantes inventées et les souvenirs qui donnent à chaque recette sa place dans la mémoire familiale. Le MVP prévoit explicitement d’enrichir les recettes d’anecdotes, de variantes et de médias.

## Principes directeurs

- **Préserver :** donner aux recettes un lieu durable où elles peuvent être retrouvées et documentées.
- **Transmettre :** faciliter le partage et la collaboration entre générations.
- **Rassembler :** faire de la cuisine un lien familial, et pas seulement une activité individuelle.
- **Rester accessible :** privilégier une expérience claire, fluide et adaptée à tous les âges.
- **Respecter la confiance :** garder les recettes privées par défaut et laisser leur propriétaire maîtriser leur partage.

## Première étape : le MVP

Le MVP donne aux familles un premier espace commun pour capturer, organiser, retrouver et partager leurs recettes, tout en les enrichissant de variantes, d’anecdotes et de médias.

## La suite

Les évolutions futures — de l’accompagnement en cuisine aux livres imprimés — devront prolonger la mémoire et la transmission familiales, sans détourner Bon App’ de sa vocation.

## Comment mesurer les progrès du MVP

Les indicateurs ci-dessous sont des cibles de travail à valider :

1. **Capture :** mesurer le temps entre la confirmation de l’import d’une photo et l’obtention d’une fiche propre, structurée et partageable ; cible : moins de 10 secondes.
2. **Centralisation :** suivre le nombre de recettes ajoutées et lues par utilisateur ; cibles : 10 recettes ajoutées au cours du premier mois après l’inscription et au moins une recette lue par mois.
3. **Transmission et mémoire :** suivre séparément la part des recettes partagées et la part des recettes enrichies d’une anecdote, d’une photo ou d’une variante ; cible de travail : au moins 25 % des recettes sont partagées ou enrichies.
