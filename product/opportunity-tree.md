# Arbre d’opportunités — première version

> Document de travail fondé sur la vision produit, les notes d’irritants et l’arbre de problèmes. L’entretien U-001 est rétrospectif et singulier : il ne permet pas de généraliser. Les formulations ci-dessous séparent les faits rapportés, les hypothèses à vérifier et les propositions de travail. Aucune hypothèse de lien causal n’est présentée comme établie.

## Faits documentés

- **Suivi d’une recette :** U-001 dit perdre parfois le fil des étapes et relire la recette. Dans un épisode distinct, il a trouvé certaines instructions d’une recette de crêpes peu claires et les a revues. Le lien entre ces deux épisodes n’est pas établi. Source : [irritants utilisateurs](./user-pain-points.md), entretien U-001 ; [arbre de problèmes](./problem-tree.md), A et C.
- **Correction et adaptation :** U-001 n’a pas inscrit dans un livre une correction de temps de cuisson, par crainte de l’abîmer. Il dit aussi copier certaines recettes et ses ajustements dans Word pour pouvoir les refaire. La relation entre ces deux pratiques n’est pas établie. Source : [irritants utilisateurs](./user-pain-points.md), IRR-001 et entretien U-001.
- **Recherche :** U-001 cite plusieurs sources et décrit où il cherche une recette à refaire, sans rapporter d’échec ni de difficulté concrète de recherche. Le [parcours actuel](./parcours-actuel.md) qualifie cette difficulté d’« à vérifier ».
- **Mémoire et transmission :** U-001 dit que la transmission papier est fragile et mentionne les recettes de ses parents dans un cahier, sans relater d’incident. La [vision produit](./vision.md) place la mémoire culinaire familiale et sa transmission au cœur de Bon App’, mais ce cadrage n’est pas une validation indépendante.

## Résultat attendu proposé

**Lorsqu’une personne suit une recette, réduire la part des séances où elle perd le fil au point de devoir relire la recette pour retrouver où elle en est.**

**Mesure proposée :** nombre de séances observées avec cet épisode, rapporté au nombre de séances observées où une personne suit une recette. Consigner également les circonstances et le recours éventuel à une relecture. Les notes actuelles ne fournissent pas de mesure de départ ; établir une référence et convenir d’une cible après les entretiens et observations. Aucun seuil chiffré n’est proposé à ce stade.

Ce résultat est une proposition centrée sur le problème le mieux étayé dans [l’arbre de problèmes](./problem-tree.md), et non un résultat déjà validé auprès d’un groupe d’utilisateurs.

## Arborescence textuelle

```text
RÉSULTAT ATTENDU [PROPOSITION]
Réduire la part des séances de suivi d’une recette où la personne perd le fil
au point de devoir relire la recette pour retrouver où elle en est.
│
├── O1. Garder le fil des étapes pendant la préparation [OPPORTUNITÉ PRIORITAIRE PROPOSÉE]
│   ├── O1.1 Mieux comprendre les instructions pendant leur réalisation
│   │   [lien avec le résultat : hypothèse à vérifier]
│   └── O1.2 Retrouver plus facilement le point où l’on en est après une perte de fil
│       [lien avec le résultat : lien plausible, effet à vérifier]
│
├── O2. Conserver une correction ou une adaptation sans risquer d’altérer la source
│   [lien avec le résultat : indirect et non établi]
│   └── O2.1 Retrouver les ajustements associés à une recette lorsqu’on la refait
│       [lien avec le résultat : hypothèse à vérifier]
│
├── O3. Retrouver une recette déjà utilisée parmi les sources actuelles
│   [lien avec le résultat : hypothèse à vérifier]
│   └── O3.1 Comprendre ce qui rend une recherche difficile, ou confirmer qu’elle l’est
│       [lien avec le résultat : hypothèse à vérifier]
│
└── O4. Préserver les recettes familiales et ce qui leur donne leur sens
    [lien avec le résultat : indirect, hypothétique]
    └── O4.1 Clarifier ce qui risque concrètement de ne pas être transmis
        [lien avec le résultat : hypothèse à vérifier]
```

Les opportunités O2 à O4 sont conservées comme pistes distinctes plutôt que fusionnées avec O1 : les sources ne démontrent pas qu’elles causent la perte du fil pendant la préparation.

## Sources, statut et lien avec le résultat

| Opportunité | Source / preuve | Statut | Lien supposé avec le résultat attendu |
|---|---|---|---|
| **O1 — Garder le fil des étapes pendant la préparation** | U-001 dit qu’il lui arrive de se perdre et qu’il relit la recette ; [irritants](./user-pain-points.md), IRR-003 ; [arbre](./problem-tree.md), A. | Fait rapporté par une personne, rétrospectivement ; fréquence et contexte précis inconnus. | Lien direct avec le résultat proposé : c’est le comportement mesuré. Généralisation à d’autres personnes à vérifier. |
| **O1.1 — Mieux comprendre les instructions pendant leur réalisation** | U-001 juge parfois peu claires des instructions de la recette de crêpes ; [irritants](./user-pain-points.md), IRR-002 ; [arbre](./problem-tree.md), C. | Fait rapporté dans un épisode ; aucune conséquence précise ni aucun lien avec la perte du fil ne sont établis. | Des instructions peu claires pourraient contribuer à perdre le fil, mais cette relation est une hypothèse à vérifier. |
| **O1.2 — Retrouver le point où l’on en est après une perte de fil** | U-001 rapporte relire la recette après s’être perdu ; [irritants](./user-pain-points.md), IRR-003. | La relecture est rapportée ; son utilité, son coût et les circonstances ne sont pas documentés. | Réduire le besoin ou l’effort de relecture pourrait améliorer la mesure du résultat ; effet à vérifier. |
| **O2 — Conserver une correction ou une adaptation sans risquer d’altérer la source** | U-001 n’a pas corrigé le livre par crainte de l’abîmer ; il copie certaines recettes avec leurs ajustements dans Word ; [irritants](./user-pain-points.md), IRR-001 et entretien U-001. | Comportements et raison rapportés ; récurrence et problème de réutilisation non documentés. | Une correction retrouvable pourrait éviter qu’une information souhaitée manque lors d’une autre préparation, mais aucun lien avec la perte du fil ou un résultat de préparation n’est établi. Hypothèse à vérifier. |
| **O2.1 — Retrouver les ajustements lors d’une nouvelle utilisation** | U-001 dit copier certaines recettes avec ses ajustements « pour pouvoir la refaire plus tard » ; [irritants](./user-pain-points.md). | Usage rapporté ; difficulté à retrouver ou à réutiliser ces ajustements non rapportée. | Pourrait contribuer au résultat si les ajustements aident à suivre la recette ; rôle non documenté, hypothèse à vérifier. |
| **O3 — Retrouver une recette déjà utilisée parmi les sources actuelles** | U-001 décrit une recherche dans Word, un autre livre ou par recherche interne/IA ; [irritants](./user-pain-points.md). Le [parcours actuel](./parcours-actuel.md) marque la difficulté de recherche « à vérifier ». | Hypothèse à vérifier : aucun échec, délai ou effort problématique n’est rapporté. | Retrouver une recette peut être une condition préalable pour la suivre, mais aucune difficulté de recherche n’est établie ; lien hypothétique. |
| **O3.1 — Comprendre ce qui rend une recherche difficile, ou confirmer qu’elle l’est** | Question non résolue dans [les irritants](./user-pain-points.md), IRR-004, et [l’arbre de problèmes](./problem-tree.md), D. | Proposition de recherche, pas un besoin utilisateur établi. | Permettrait de déterminer si cette piste contribue réellement au résultat ; lien à valider avant de la prioriser. |
| **O4 — Préserver les recettes familiales et ce qui leur donne leur sens** | U-001 qualifie de fragile la transmission papier ; [irritants](./user-pain-points.md), IRR-005. La vision produit évoque recettes, gestes, variantes et souvenirs ; [vision](./vision.md). | Préoccupation rapportée sans incident ; la vision est un cadrage produit, pas une preuve d’impact utilisateur. | La préservation pourrait maintenir des recettes disponibles pour être suivies, mais aucune perte ni conséquence sur la préparation n’est rapportée. Lien indirect et hypothétique. |
| **O4.1 — Clarifier ce qui risque concrètement de ne pas être transmis** | Aucune perte concrète rapportée ; question ouverte dans [les irritants](./user-pain-points.md), IRR-005. | Hypothèse à vérifier. | Aiderait à évaluer si la préservation a un effet sur le résultat prioritaire ou relève d’un résultat distinct ; lien à valider. |

## Opportunité prioritaire proposée : pistes de solution et hypothèses à tester

O1 est prioritaire pour cette première exploration parce qu’il correspond au signal utilisateur le plus directement formulé dans les sources, non parce que son importance pour l’ensemble des utilisateurs est démontrée.

Les pistes ci-dessous sont des propositions à comparer, pas des fonctionnalités décidées :

| Piste de solution possible | Hypothèse à tester | Comment l’explorer |
|---|---|---|
| Clarifier et mieux séquencer le texte d’une recette, sans changer l’information culinaire. | Des formulations ambiguës ou des consignes regroupant plusieurs actions contribuent à la perte du fil. Le lien entre clarté et perte du fil n’est pas encore établi. | Faire suivre une recette comparable dans sa version actuelle puis dans une version reformulée ; relever les hésitations, pertes de fil et relectures, puis demander ce qui les a provoquées. |
| Présenter les étapes de façon à rendre plus facile le repérage de l’étape en cours tout en laissant le contexte nécessaire accessible. | La difficulté vient en partie du repérage de sa position, indépendamment de la clarté du texte. | Comparer des maquettes papier ou prototypes avec le même contenu ; observer si la personne retrouve l’étape en cours et comprendre les écarts. |
| Permettre à la personne d’externaliser où elle en est pendant la recette. | Se souvenir de l’avancement augmente l’effort ou provoque certaines relectures ; un repère externe pourrait réduire cet effort. | Tester un repère simple en situation de préparation et vérifier s’il est spontanément utile, ignoré ou gênant. |

Ces essais doivent commencer par un cas concret et observer le comportement avant d’interpréter une préférence déclarée. Si les entretiens montrent que la perte du fil n’est pas prioritaire, que la cause supposée est différente ou que les pistes n’améliorent pas le résultat mesuré, réviser O1 et son résultat attendu.

## À ne pas conclure à ce stade

- La dispersion des recettes ne prouve pas une difficulté de recherche.
- Le souhait de modifier, de conserver ou de partager une recette ne prouve pas à lui seul un besoin non satisfait.
- La fragilité évoquée de la transmission papier ne prouve pas qu’une recette, une variante ou un souvenir a été perdu.
- Une instruction parfois peu claire n’est pas une cause établie de la perte du fil.
- Les mesures et objectifs de la [vision produit](./vision.md) sont des cibles de travail à valider ; ils ne constituent pas une référence mesurée pour le résultat proposé ici.
