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

## Bénéfices attendus

Ces bénéfices expriment les changements recherchés, pas des résultats déjà obtenus. Le premier s’appuie sur un irritant rapporté par une personne ; les autres restent des hypothèses à valider. Les indicateurs, situations de départ, cibles et conditions détaillés figurent dans le [business case](./business-case.md).

- **Mieux garder le fil en cuisinant.** Les personnes qui suivent une recette pourraient perdre moins souvent leur place et avoir moins besoin de la relire. Signal individuel rapporté par U-001 ; fréquence, impact et généralisation à vérifier.
- **Rassembler et retrouver ses recettes.** Les personnes et familles pourraient conserver leurs recettes dans un espace commun et les réutiliser plus facilement. Le souhait d’un support unique est exprimé, mais une difficulté concrète de recherche n’est pas établie.
- **Retrouver ses adaptations.** Les cuisiniers qui modifient une recette pourraient retrouver leurs ajustements lorsqu’ils la refont. U-001 conserve certaines adaptations dans Word ; aucun échec de conservation ou de recherche n’est rapporté.
- **Préserver et transmettre la mémoire familiale.** Les familles pourraient partager leurs recettes avec les variantes, anecdotes et savoir-faire associés. Cette ambition est au cœur de la vision ; l’intérêt, les incidents évités et l’effet sur la transmission restent à vérifier.

## Objectifs produit

Un objectif décrit un changement recherché pour les utilisateurs, pas une fonctionnalité à développer ni un livrable à produire. L’ordre ci-dessous privilégie d’abord la force des éléments disponibles ; il ne constitue pas une priorité validée auprès d’un groupe d’utilisateurs.

### 1. Aider les personnes à garder le fil lorsqu’elles cuisinent

- **Résultat recherché :** réduire la part des séances où une personne perd le fil des étapes et doit relire la recette pour reprendre.
- **Bénéficiaire :** personnes qui suivent une recette pendant la préparation.
- **Justification sourcée :** U-001 rapporte que cela lui arrive et qu’il relit la recette ([Irritants utilisateurs](./user-pain-points.md), IRR-003). C’est un signal rétrospectif individuel ; sa fréquence, son impact et sa généralisation restent à vérifier.
- **Indicateur :** part des séances observées comportant une perte du fil suivie d’une relecture.
- **Situation actuelle :** aucun relevé ni observation directe ; seule l’expérience rapportée par U-001 est disponible.
- **Cible :** à mesurer, puis à définir après établissement d’une référence.
- **Échéance :** à définir avant le pilote.
- **Garde-fou :** vérifier que la baisse des relectures ne s’accompagne pas d’une moins bonne compréhension des instructions ou d’erreurs de préparation ; préserver l’accessibilité.

### 2. Aider les familles à retrouver leurs recettes conservées

- **Résultat recherché :** augmenter la part des membres qui peuvent retrouver et consulter une recette conservée dans leur espace familial.
- **Bénéficiaire :** personnes qui conservent ou veulent refaire des recettes, et familles qui souhaitent les rassembler.
- **Justification sourcée :** U-001 cite plusieurs sources, copie certaines recettes dans Word et exprime le souhait d’un support unique. Il ne rapporte toutefois aucun échec concret de recherche ([Irritants utilisateurs](./user-pain-points.md), IRR-004). Le bénéfice reste donc une hypothèse.
- **Indicateur :** part des personnes ou familles actives ayant ajouté une recette consultable et l’ayant relue ; compléter par la réussite d’une tâche de recherche.
- **Situation actuelle :** aucun niveau de référence ni taux de réussite de recherche n’est documenté.
- **Cible :** la vision propose comme repères de travail **10 recettes ajoutées au premier mois après inscription** et **au moins une recette lue par mois**. Ces repères sont à valider et ne prouvent pas, à eux seuls, qu’une recette est facilement retrouvée.
- **Échéance :** mesurer au cours du premier mois après inscription, conformément au repère existant ; date du pilote à définir.
- **Garde-fou :** mesurer la réussite de recherche, pas seulement le nombre de recettes ajoutées ou lues ; garder les recettes privées par défaut et vérifier les droits d’accès.

### 3. Aider les familles à transmettre les recettes et leur contexte

- **Résultat recherché :** augmenter la part des familles où une recette et les éléments qui lui donnent son sens — variante, anecdote ou savoir-faire — sont effectivement partagés ou enrichis.
- **Bénéficiaire :** personnes qui souhaitent transmettre leur patrimoine culinaire et membres de la famille qui le reçoivent.
- **Justification sourcée :** la mémoire familiale et la transmission sont au cœur de la vision. U-001 juge fragile la transmission papier, mais aucun incident de perte ou de transmission manquée n’est rapporté ([Irritants utilisateurs](./user-pain-points.md), IRR-005). Le bénéfice reste à valider.
- **Indicateur :** part des familles ayant un exemple concret de recette ou de savoir-faire partagé ; suivre séparément les parts de recettes partagées et enrichies.
- **Situation actuelle :** aucune mesure de partage entre générations ni de transmission utile n’est disponible.
- **Cible :** la vision mentionne **25 % des recettes partagées ou enrichies** comme cible de travail. Cette cible combinée est à valider ; ses dénominateurs et ses seuils séparés restent à définir.
- **Échéance :** à définir selon le cycle nécessaire à une transmission réelle ; aucune échéance n’est documentée.
- **Garde-fou :** ne pas assimiler un partage technique à une transmission utile ; le partage doit rester explicite, contrôlé et révocable, sans imposer l’ajout d’anecdotes ou de médias.

**Fonctionnalités et livrables — à distinguer des objectifs :** le suivi des étapes, la capture photo/OCR, l’espace familial, la recherche et les champs de variantes sont des moyens possibles, non des objectifs en soi. Un prototype, une application web/mobile/API ou un rapport de test sont des livrables. Leur réalisation ne démontre pas à elle seule qu’un objectif utilisateur est atteint.

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

## Mesure des progrès du MVP

Les indicateurs et cibles de travail, leur niveau de preuve et leurs conditions de mesure sont regroupés dans le [business case](./business-case.md). Ils devront être confirmés avant d’être considérés comme des engagements.
