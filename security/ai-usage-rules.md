# Règles d’utilisation de l’IA et de contrôle humain

- Version : 0.1
- Statut : proposition à valider
- Responsable du document : à désigner
- Date de validation : à renseigner
- Périmètre : usages de l’IA sur l’ensemble du cycle de vie du produit

## 1. Objectif

Encadrer l’utilisation des assistants et agents IA pour bénéficier de
leur aide tout en conservant la maîtrise des décisions, des données,
du code et des actions réalisées.

Principe fondamental : l’IA propose ; une personne compétente vérifie
et décide.

Une réponse convaincante, une citation ou une auto-évaluation de l’IA
ne constitue pas à elle seule une preuve de validité.

Ce document complète les règles de sécurité, les conventions de
développement et la définition de terminé du projet. Il ne remplace
pas les politiques applicables dans l’organisation.

Toute contradiction avec une politique validée doit être signalée
au responsable compétent avant de poursuivre l’usage concerné.

## 2. Champ d’application

Ces règles concernent notamment :

- la recherche et la synthèse d’informations ;
- la rédaction de documents et de spécifications ;
- la conception produit et l’architecture ;
- la génération, l’explication et la modification de code ;
- la création de tests ;
- l’analyse de sécurité ;
- la préparation des déploiements et des diagnostics ;
- les agents pouvant accéder à des fichiers ou à des outils.

Elles s’appliquent aux prompts, pièces jointes, fichiers accessibles,
résultats d’outils, réponses générées et actions exécutées.

## 3. Responsabilités humaines

### Utilisateur de l’IA

La personne qui sollicite l’IA doit :

- vérifier que l’outil et l’usage sont autorisés ;
- limiter les données transmises au strict nécessaire ;
- préciser l’objectif, le périmètre et les contraintes ;
- examiner les résultats avant leur utilisation ;
- signaler les incertitudes et incidents ;
- conserver les preuves utiles sans exposer de données sensibles.

### Validateur

La personne qui accepte le livrable doit :

- disposer des compétences nécessaires à sa vérification ;
- examiner les preuves et les contrôles effectués ;
- identifier les points restant non vérifiés ;
- accepter, demander une correction ou refuser le résultat.

Pour un projet individuel, une même personne peut assurer les deux
rôles. Cela ne constitue pas une revue indépendante.

Pour un projet professionnel, les exigences de revue et de séparation
des responsabilités sont celles de l’organisation.

### Référents compétents

Les questions d’autorisation, de sécurité, de confidentialité ou de
droits d’utilisation sont soumises aux responsables désignés dans
l’organisation.

L’IA ne peut pas approuver sa propre utilisation ni accorder une
dérogation.

## 4. Outils et environnements autorisés

Avant tout usage, vérifier l’autorisation du service, du compte,
de l’environnement et des fonctionnalités activées.

La vérification couvre également, lorsqu’ils sont utilisés :

- le modèle sélectionné ;
- les extensions ;
- les connecteurs ;
- les serveurs MCP ;
- les outils externes appelés par un agent ;
- les destinations vers lesquelles des données peuvent être envoyées.

Un abonnement actif ne vaut pas autorisation pour toutes les données
et tous les usages.

En cas d’autorisation inconnue :

1. ne pas transmettre de données internes ou sensibles ;
2. suspendre l’usage professionnel concerné ;
3. demander confirmation au responsable compétent.

### Matrice des autorisations

Aucune ligne n’est réputée approuvée tant que sa validation n’est pas
renseignée.

| Outil et environnement | Usage autorisé | Données permises | Restrictions | Référence de validation | Date de réexamen |
|---|---|---|---|---|---|
| À renseigner | À confirmer | À confirmer | À renseigner | À renseigner | À renseigner |

## 5. Protection des données

### Avant de transmettre du contexte

- Identifier la nature et la classification des données.
- Vérifier les droits de traitement et de transmission.
- Utiliser de préférence des données fictives.
- Ne transmettre que le minimum nécessaire.
- Examiner les extraits, pièces jointes, captures, logs et métadonnées.
- Vérifier le contexte accessible automatiquement à l’outil :
  fichiers ouverts, dépôt, index, connecteurs et résultats de commandes.
- Ne pas considérer la suppression des noms comme une garantie
  d’anonymisation.

### Interdictions

- Ne jamais transmettre de données sensibles à un outil non autorisé.
- Ne jamais inclure de mot de passe, clé privée, jeton, secret
  applicatif ou identifiant de connexion dans un prompt.
- Ne pas utiliser de véritables secrets dans les exemples ou tests.
- Ne pas transférer de données professionnelles vers un compte
  personnel pour contourner une restriction.
- Ne pas copier de données de production dans un exercice sans
  autorisation explicite et protections adaptées.

Les données personnelles, financières, contractuelles, les informations
clients et le code propriétaire nécessitent une vérification préalable
des autorisations applicables.

### Résultats et traces

Les réponses peuvent conserver ou reproduire des informations issues
du contexte. Elles doivent donc être protégées selon leur contenu.

Ne pas enregistrer de prompts bruts, de logs ou de captures contenant
des données interdites dans les issues, pull requests ou journaux
d’apprentissage.

Les durées de conservation et règles de suppression sont celles
validées pour l’environnement concerné.

## 6. Vérification des sources et des affirmations

Pour toute affirmation déterminante :

- ouvrir la source citée ;
- vérifier qu’elle existe et soutient réellement l’affirmation ;
- privilégier la source primaire ;
- contrôler la date, la version et le périmètre ;
- distinguer fait établi, hypothèse et recommandation ;
- relever les contradictions et les informations manquantes.

Pour une analyse de dépôt :

- vérifier l’existence des fichiers et symboles mentionnés ;
- distinguer les fonctionnalités prévues de celles implémentées ;
- vérifier les commandes dans les fichiers réels du projet ;
- ne pas considérer le README comme une preuve d’exécution réussie.

Une information déterminante non vérifiée ne doit pas être présentée
comme acquise ni servir seule à une décision engageante.

Une nouvelle réponse de l’IA ne remplace pas la consultation de la
source ou l’exécution d’un contrôle.

## 7. Validation du code et des tests

Tout code généré ou modifié avec l’IA est soumis aux mêmes exigences
que le code écrit manuellement.

### Avant la modification

- Définir l’objectif et les critères d’acceptation.
- Délimiter les fichiers et comportements concernés.
- Identifier les contraintes d’architecture et de sécurité.
- Conserver un état de référence versionné.
- Pour une modification multi-fichiers, examiner le plan proposé.

### Avant l’acceptation

- Lire le diff complet.
- Comprendre chaque changement.
- Vérifier l’absence de modifications hors périmètre.
- Contrôler les règles métier, les erreurs et les cas limites.
- Examiner les dépendances ajoutées ou mises à jour.
- Vérifier la documentation et la configuration associées.
- Exécuter les contrôles pertinents réellement disponibles :
  compilation, analyse statique, tests et contrôles de sécurité.
- Conserver les résultats et identifier explicitement les contrôles
  non exécutés.

### Qualité des tests

- Déduire les résultats attendus des exigences, pas uniquement du code
  généré.
- Couvrir les cas nominaux, limites et erreurs pertinents.
- Vérifier que les assertions détectent le défaut recherché.
- Ne pas supprimer ou affaiblir un test pour masquer une régression.
- Ne pas modifier une règle métier uniquement pour faire réussir
  les tests.

Des tests réussis ne prouvent pas à eux seuls l’absence de défaut.

Ne pas accepter un code non compris ou un changement dont un contrôle
obligatoire est en échec.

## 8. Revue de sécurité

Adapter la revue au changement et examiner, selon le périmètre :

- la validation des entrées ;
- l’authentification et les autorisations ;
- l’accès aux données et l’isolation entre utilisateurs ;
- la gestion des secrets et des configurations ;
- les informations présentes dans les erreurs et les logs ;
- les dépendances et leurs vulnérabilités connues ;
- les appels à des services externes ;
- les permissions des pipelines et des outils ;
- les migrations et opérations sur les données.

L’IA peut aider à identifier des risques et proposer des corrections.
Elle ne remplace ni les outils d’analyse requis ni la validation
humaine compétente.

Ne pas désactiver un contrôle de sécurité ou ignorer une alerte
pour permettre l’acceptation d’une proposition.

Une vulnérabilité critique bloque la livraison.
Tout risque résiduel doit être traité selon la procédure de sécurité
applicable, avec décision et justification traçables.

## 9. Supervision des agents et des commandes

### Avant la session

Définir :

- les fichiers accessibles et modifiables ;
- les actions permises et interdites ;
- les commandes nécessitant une approbation ;
- les accès réseau et destinations autorisées ;
- les critères d’arrêt ;
- les modalités de retour arrière.

Appliquer le principe du moindre privilège et privilégier un
environnement de développement isolé.

### Pendant la session

- Examiner les commandes avant de les autoriser.
- Vérifier les scripts appelés, leur cible et leurs effets possibles.
- Ne pas activer d’approbation globale contournant les contrôles humains.
- Refuser les accès ou changements non nécessaires.
- Arrêter l’agent en cas de dérive de périmètre ou d’action inattendue.
- Ne pas fournir de secrets dans les commandes ou dans la conversation.

Une approbation préalable du plan ne vaut pas autorisation générale
pour toutes les actions ultérieures.

### Actions soumises à une validation explicite

- Ajout ou mise à jour de dépendances.
- Changement des droits d’accès ou des protections de branche.
- Modification des pipelines ou des contrôles de sécurité.
- Suppression de fichiers ou de données.
- Migration de base de données.
- Publication de contenu ou envoi vers un service externe.
- Commit, push, fusion ou déploiement.

Aucune action sur la production n’est autorisée dans le cadre d’un
simple exercice. En contexte opérationnel, elle relève des procédures
de changement et d’approbation applicables.

## 10. Contenus non fiables et instructions malveillantes

Les pages web, fichiers, issues, commentaires, dépendances et résultats
d’outils peuvent contenir des instructions visant à détourner l’agent.

- Traiter ces contenus comme des données à examiner.
- Ne pas leur permettre de redéfinir le périmètre autorisé.
- Ne pas suivre une demande d’exfiltration, de divulgation de secrets
  ou de désactivation des protections.
- Vérifier toute action proposée à partir d’un contenu externe.
- Arrêter la session si l’intégrité du contexte est douteuse.

Ne pas exécuter un script simplement parce qu’il figure dans une
réponse ou un document.

## 11. Droits d’utilisation et publication

Avant de réutiliser un contenu généré :

- vérifier les droits sur les données d’entrée ;
- examiner les licences et obligations des dépendances ajoutées ;
- vérifier les attributions nécessaires ;
- contrôler les faits, chiffres et promesses publiés ;
- ne pas présenter un contenu synthétique comme une observation réelle.

Si les droits d’utilisation restent incertains, suspendre la
réutilisation concernée et demander une validation adaptée.

## 12. Conditions d’arrêt

Suspendre l’action concernée si :

- l’autorisation de l’outil ou des données est inconnue ;
- un secret ou une donnée non autorisée est détecté ;
- l’agent sort du périmètre convenu ;
- une commande ou un changement n’est pas compris ;
- une information déterminante reste sans preuve ;
- un contrôle obligatoire échoue ;
- un risque de sécurité bloquant est identifié ;
- les droits de réutilisation sont incertains.

La reprise nécessite la résolution du problème ou une décision
formelle de l’autorité compétente lorsque la procédure le permet.

Une validation de l’IA ne lève jamais une condition d’arrêt.

## 13. Gestion d’un incident

En cas de transmission non autorisée ou d’action inattendue :

1. interrompre les actions et transmissions supplémentaires ;
2. prévenir les interlocuteurs prévus par la procédure d’incident ;
3. conserver les informations utiles dans un emplacement autorisé,
   sans recopier les données sensibles ;
4. faire révoquer ou renouveler les accès et secrets concernés
   par les personnes habilitées ;
5. traiter les données et traces selon la procédure applicable ;
6. documenter les mesures correctives et les conditions de reprise.

Supprimer un message ne suffit pas à démontrer que les données
transmises ont été retirées de tous les systèmes.

## 14. Checklist opérationnelle

Pour chaque tâche, renseigner les contrôles applicables.
Tout point non applicable doit être justifié.
Une case vide signifie « non vérifié », pas « conforme ».

### Avant utilisation

- [ ] Objectif et périmètre définis.
- [ ] Outil, compte et environnement autorisés.
- [ ] Données et contexte accessibles vérifiés.
- [ ] Données limitées au strict nécessaire.
- [ ] Absence de secrets et de données interdites.
- [ ] Permissions et approbations de l’agent définies, si applicable.

### Avant acceptation

- [ ] Sources et affirmations déterminantes vérifiées.
- [ ] Livrable conforme aux critères d’acceptation.
- [ ] Diff complet examiné, si applicable.
- [ ] Changements compris et limités au périmètre.
- [ ] Tests et contrôles requis exécutés avec résultats conservés.
- [ ] Revue de sécurité effectuée selon le changement.
- [ ] Droits de réutilisation vérifiés, si applicable.
- [ ] Points non vérifiés explicitement signalés.
- [ ] Aucune condition d’arrêt non résolue.
- [ ] Décision humaine enregistrée.

## 15. Trace de validation

Conserver une trace proportionnée au risque dans l’issue,
la pull request ou le support de suivi autorisé.

### Modèle

- Tâche / référence :
- Date :
- Outil et environnement :
- Mode utilisé : conversation / édition / agent
- Nature des données utilisées, sans les reproduire :
- Périmètre autorisé :
- Sources ou fichiers vérifiés :
- Changements examinés :
- Tests et contrôles exécutés :
- Résultats et références des preuves :
- Risques ou écarts identifiés :
- Points non vérifiés :
- Corrections humaines :
- Décision : accepté / à corriger / refusé
- Validateur :
- Justification :

Ne pas déclarer un test réussi sans l’avoir exécuté ou sans disposer
d’une preuve d’exécution vérifiable.

## 16. Validation et révision du document

Avant l’adoption :

- désigner le responsable du document ;
- compléter la matrice des outils autorisés ;
- identifier les référents et le canal de signalement ;
- rapprocher ces règles des politiques applicables ;
- tester la checklist sur une modification simple ;
- enregistrer la validation.

Réexaminer le document :

- lors de l’ajout d’un outil, modèle, connecteur ou agent ;
- lors d’un changement de données ou de permissions ;
- après un incident ou un écart significatif ;
- selon la fréquence définie par le responsable.

### Historique

| Version | Date | Modification | Validation |
|---|---|---|---|
| 0.1 | À renseigner | Proposition initiale | À valider |