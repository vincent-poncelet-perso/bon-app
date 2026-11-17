# Arbre de problèmes — première version

> Document de travail à réviser après les entretiens utilisateurs. Les notes disponibles reposent principalement sur un entretien rétrospectif avec U-001 ; elles ne permettent pas de généraliser. Les liens causaux ne sont retenus que lorsqu’ils sont explicitement rapportés. Une branche « hypothèse à vérifier » n’affirme pas que le lien existe.

## Arborescence textuelle

### A — Perdre le fil en suivant une recette (problème central le mieux étayé)

```text
Problème central : U-001 dit qu’il lui arrive de perdre le fil des étapes quand il suit une recette.

├── Causes directes  
│   ├── Non documentées.  
│   └── Instructions parfois peu claires dans un épisode distinct (recette de crêpes) : lien avec la perte du fil non établi.  
├── Causes profondes  
│   └── Non documentées.  
└── Conséquences / réactions rapportées  
    ├── U-001 relit la recette après s’être perdu (lien explicitement rapporté).  
    ├── U-001 prend parfois des notes pour faciliter la réalisation ; lien avec cette difficulté et effet non précisés.  
    └── Effet sur le déroulement ou le résultat de la préparation : inconnu.  
```

### B — Ne pas inscrire une correction dans un livre (problème central distinct)

```text
Problème central : dans un cas, U-001 souhaitait corriger le temps de cuisson d’une recette imprimée, mais ne l’a pas fait.

├── Cause directe
│   └── Crainte d’abîmer le livre (raison explicitement donnée par U-001 pour ne pas modifier la recette dans ce livre).
├── Causes profondes
│   └── Non documentées.
└── Conséquence rapportée
    └── La correction n’est pas inscrite dans le livre ; correction éventuelle ailleurs et conséquence sur le plat inconnues.
```

### C — Instructions parfois peu claires (problème central distinct)

```text
Problème central : U-001 juge parfois peu claires certaines instructions d’une recette de crêpes.

├── Causes directes et profondes
│   └── Non documentées.
└── Conséquences / réactions
    ├── U-001 dit avoir revu les instructions ; le lien exact avec leur manque de clarté n’est pas explicité.
    └── Effet sur la préparation ou son résultat : inconnu.
```

### D — Difficulté à retrouver une recette (candidat non confirmé)

```text
Problème central à valider : les recettes provenant de plusieurs sources seraient difficiles à retrouver.

├── Causes possibles
│   └── Multiplicité des sources citée par U-001 ; aucune difficulté de recherche qui en découlerait n’est décrite.
├── Causes profondes
│   └── Non documentées.
└── Conséquences
    └── Aucune conséquence d’un échec ou d’un effort excessif de recherche n’est rapportée. Le parcours actuel évoque cette difficulté comme étant à vérifier.
```

### E — Fragilité de la transmission papier (candidat non confirmé)

```text
Problème central à valider : U-001 qualifie de fragile la transmission des recettes familiales sur papier.

├── Causes directes et profondes
│   └── Non documentées ; aucun incident concret n’est cité.
└── Conséquences
    └── Aucune perte ou conséquence vécue n’est rapportée.
```

## Tableau de validation

| Élément | Type | Preuve disponible | Statut | Question de validation |
|---|---|---|---|---|
| Perdre parfois le fil des étapes en suivant une recette | Problème central A | U-001 dit « il m’arrive de me perdre » ; [irritants utilisateurs](./user-pain-points.md), entretien U-001 ; [problèmes utilisateurs](./problem-statements.md), analyse | Rapporté par une personne, rétrospectivement ; fréquence et contexte précis inconnus | Quel est le dernier exemple concret ? À quel moment et dans quelles circonstances le fil est-il perdu ? |
| Instructions parfois peu claires | Problème central C / facteur possible pour A | Épisode de la recette de crêpes, [irritants utilisateurs](./user-pain-points.md) et [problèmes utilisateurs](./problem-statements.md) | Signal rapporté pour un épisode ; aucun lien établi avec A | Quelles instructions n’étaient pas claires ? Cela a-t-il fait perdre le fil ou entraîné une autre difficulté ? |
| Relire la recette après avoir perdu le fil | Conséquence / réaction de A | U-001 dit « alors je la relis à nouveau » ; [irritants utilisateurs](./user-pain-points.md) | Lien explicitement rapporté ; efficacité de la relecture inconnue | La relecture permet-elle de reprendre ? Que se passe-t-il ensuite ? |
| Prendre parfois des notes pour faciliter la réalisation | Réaction possible à A | Déclaration de U-001 dans [l’entretien](./user-pain-points.md) | Pratique rapportée ; lien avec A et effet non documentés | Dans quelle situation les notes sont-elles prises, et quel effet ont-elles ? |
| Crainte d’abîmer le livre | Cause directe de B | U-001 explique ne pas avoir modifié la recette « pour ne pas abîmer le livre » ; [irritants utilisateurs](./user-pain-points.md) | Cause explicitement donnée pour un cas seulement | Cette crainte apparaît-elle avec d’autres recettes ou supports ? |
| Correction non inscrite dans le livre | Conséquence de B | Même épisode de l’entretien U-001 ; [problèmes utilisateurs](./problem-statements.md) | Rapportée pour un cas ; correction ailleurs et effet sur le plat inconnus | La correction a-t-elle été notée ailleurs ? Quelle conséquence a eu son absence dans le livre ? |
| Multiplicité des sources de recettes | Contexte possible de D, pas une cause démontrée | U-001 cite livres, Internet, IA, cahiers, SMS/WhatsApp et Word ; [irritants utilisateurs](./user-pain-points.md) | Contexte rapporté ; difficulté de recherche non établie | Racontez la dernière recherche d’une recette déjà utilisée : a-t-elle été retrouvée, où et avec quel effort ? |
| Difficulté à retrouver une recette | Problème central D à tester | Le [parcours actuel](./parcours-actuel.md) mentionne « Recette difficile à retrouver », dans la colonne « Difficulté à vérifier » | Hypothèse à vérifier ; aucun échec de recherche rapporté par U-001 | Y a-t-il eu un échec récent ? Quel temps, quelles étapes et quelle conséquence ? |
| Fragilité de la transmission papier | Problème central E à tester | Appréciation de U-001 dans [l’entretien](./user-pain-points.md) ; des recettes de ses parents sont conservées dans un cahier | Préoccupation rapportée, sans incident ni conséquence décrits | Quelle situation vécue ou redoutée rend cette transmission fragile ? Une recette, une variante ou une histoire a-t-elle été perdue ou manqué de l’être ? |
| Causes profondes des problèmes A, B, C, D et E | Cause profonde | Aucune source disponible n’en établit | Inconnu ; à explorer sans présupposer de cause | Quels facteurs la personne décrit-elle elle-même dans un exemple concret ? |

## Sources et limites

- [Irritants utilisateurs](./user-pain-points.md) : notes rétrospectives de l’entretien U-001.
- [Problèmes utilisateurs](./problem-statements.md) : synthèse des preuves et de leurs limites.
- [Parcours actuel](./parcours-actuel.md) : parcours formulé en étapes ; ses difficultés sont explicitement marquées « à vérifier » et ne constituent pas une observation directe.
- [Vision produit](./vision.md) : le cadrage sur la dispersion et la transmission est une hypothèse de projet, non une validation indépendante.

Les problèmes A, B et C sont des signaux limités à U-001 et aux épisodes rapportés. D et E restent des candidats de recherche, pas des problèmes établis. Cet arbre ne conclut pas que ces problèmes partagent une cause.
