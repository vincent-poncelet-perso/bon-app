# Analyse SWOT provisoire — Bon App’

**Date de l’analyse : 6 novembre 2026**  
**Périmètre :** analyse documentaire de la vision produit, de la matrice concurrentielle et des contraintes produit/techniques disponibles. Cette SWOT n’est ni une validation du marché ni un bilan d’un produit déjà livré.

## Méthode et statut

- **Forces et faiblesses** : éléments internes au projet, notamment son cadrage, son état de préparation et ses choix documentés.
- **Opportunités et menaces** : éléments de l’environnement concurrentiel ou des dépendances externes. Une fonction concurrente documentée ne prouve pas, à elle seule, une opportunité ou une menace commerciale.
- **Fait documenté** signifie que les documents du projet ou les sources concurrentielles citées rapportent directement l’élément. Cela ne valide pas les affirmations marketing, les besoins utilisateurs ni le fonctionnement en usage.
- **Hypothèse** signifie que la conséquence ou l’interprétation doit être testée. Les intentions et personas du projet ne sont pas assimilés à des besoins validés.

## Forces — facteurs internes

| # | Formulation | Source | Statut | Conséquence pour le projet | Vérification nécessaire |
|---|---|---|---|---|---|
| F1 | La vision formule explicitement Bon App’ autour de la préservation et de la transmission du patrimoine culinaire familial, y compris les gestes, variantes et souvenirs associés aux recettes. | [Vision produit](../vision.md), consultée le 06/11/2026. | **fait documenté** | Fournit un principe de cadrage distinct d’un simple inventaire de recettes et un repère pour arbitrer les fonctions. Cela ne prouve pas que cette promesse est distinctive ou recherchée par les utilisateurs. | Tester la compréhension et la valeur perçue de cette promesse auprès de familles de générations et de profils variés ; confronter le positionnement aux parcours concurrents complets. |
| F2 | Les documents distinguent un MVP (capturer, organiser, retrouver, partager et enrichir les recettes) de fonctions ultérieures, notamment l’assistant de cuisine et le livre imprimé. | [Vision produit](../vision.md) et [spécification v2.1](./Document-de-spécifications-produit-v2.1.pptx), consultées le 06/11/2026. | **fait documenté** | Cette séparation peut aider à prioriser et à limiter le périmètre initial, malgré une vision fonctionnelle large. | Faire valider un périmètre MVP unique, ses critères d’acceptation, ses dépendances et la liste explicite des fonctions reportées. |
| F3 | Des cibles de travail sont proposées pour la capture, la centralisation et l’enrichissement/partage des recettes, dont moins de 10 secondes pour une capture structurée et partageable. | [Vision produit](../vision.md), consultée le 06/11/2026. | **fait documenté** | Donne un point de départ pour concevoir des expériences et mesurer le produit plutôt que de s’en tenir à des intentions qualitatives. Les seuils restent des cibles, pas des résultats. | Définir les événements, les dénominateurs et les conditions de mesure ; tester la faisabilité et la pertinence des seuils avec un prototype et des utilisateurs. |

## Faiblesses — facteurs internes

| # | Formulation | Source | Statut | Conséquence pour le projet | Vérification nécessaire |
|---|---|---|---|---|---|
| F1 | Le dépôt décrit les applications et les tests comme des emplacements sans implémentation confirmée ; il ne documente pas de commandes d’installation, de lancement ou de test. | [Checklist de démarrage](../getting-started-checklist.md), consultée le 06/11/2026. | **fait documenté** | La valeur produit et la faisabilité technique ne sont pas encore démontrées par un produit exécutable ; les affirmations fonctionnelles restent des intentions. | Vérifier l’état du dépôt et des environnements de travail au moment du lancement ; établir un premier parcours vertical démontrable avant de promettre la disponibilité des fonctions. |
| F2 | Les personas, le problème de dispersion des recettes et les indicateurs de succès figurent dans les documents, mais aucune recherche utilisateur ou mesure de validation n’est rapportée dans les sources examinées. | [Vision produit](../vision.md), [spécification v2.1](./Document-de-spécifications-produit-v2.1.pptx) et [checklist de démarrage](../getting-started-checklist.md), consultées le 06/11/2026. | **fait documenté** | Le cadrage peut refléter des hypothèses de l’équipe plutôt que des besoins, comportements ou critères de réussite établis. | Mener des entretiens et tests de parcours avec des personnes correspondant aux profils visés ; documenter les résultats et réviser les personas, le problème et les indicateurs. |
| F3 | Plusieurs choix nécessaires à une mise en œuvre restent ouverts : OCR et structuration, authentification, hébergement, fournisseur de stockage, mode hors ligne et résolution des conflits, entre autres. | [Pile technique](../architecture/technology-stack.md), consultée le 06/11/2026. | **fait documenté** | Les coûts, performances, délais et risques de confidentialité des parcours centraux ne peuvent pas encore être estimés avec assurance ; les dépendances peuvent influer sur le périmètre MVP. | Prendre les décisions par étapes avec critères, budget et responsables ; benchmarker l’OCR sur des exemples représentatifs et spécifier le mode hors ligne avant engagement. |
| F4 | Le projet vise une expérience web, iOS et Android cohérente, tout en dépendant de capacités de plateforme différentes pour la caméra, l’import, le partage et les notifications. | [Pile technique](../architecture/technology-stack.md) et [règles d’architecture](../architecture/architecture-rules.md), consultées le 06/11/2026. | **hypothèse** | Cette contrainte pourrait accroître le coût de conception, de développement et de test, ou créer des écarts de parcours entre plateformes. | Prototyper les parcours critiques sur les trois plateformes ; mesurer les écarts et valider des solutions de repli avant de figer les critères de parité. |

## Opportunités — facteurs externes

| # | Formulation | Source | Statut | Conséquence pour le projet | Vérification nécessaire |
|---|---|---|---|---|---|
| O1 | **Hypothèse :** des familles pourraient valoriser un espace qui rassemble recettes, auteurs, variantes et souvenirs issus de supports variés, au-delà de la simple sauvegarde d’une recette. Les documents du projet décrivent ce contexte, mais ne fournissent pas de preuve de demande indépendante. | [Vision produit](../vision.md) et [spécification v2.1](./Document-de-spécifications-produit-v2.1.pptx), consultées le 06/11/2026. | **hypothèse** | Si cette valeur est confirmée, elle pourrait orienter le produit vers la mémoire et la transmission familiales plutôt que vers la seule organisation de repas. | Vérifier les pratiques actuelles, les problèmes rencontrés et les solutions de contournement auprès de familles ; tester la valeur des variantes et des anecdotes séparément des fonctions de capture. |
| O2 | **Hypothèse :** une différenciation pourrait être explorée autour de la continuité des contributions familiales et de la mémoire attachée aux recettes. La matrice montre toutefois que certains concurrents annoncent déjà partage familial, collaboration, recettes familiales ou scan ; aucun espace libre n’est établi. | [Matrice concurrentielle](./matrice-concurrentielle.md), sources concurrentielles consultées le 05/11/2026 ; [vision produit](../vision.md), consultée le 06/11/2026. | **hypothèse** | Une piste de positionnement existe à tester, mais l’import ou le partage seuls ne suffiraient pas à démontrer une différenciation. | Comparer les parcours réels et les conditions de partage des concurrents ; tester des prototypes de provenance, d’historique des variantes et d’anecdotes sans supposer qu’ils sont préférés. |
| O3 | **Hypothèse :** les offres freemium et payantes observées chez certains comparables peuvent fournir des repères pour expérimenter une monétisation, mais elles ne démontrent ni volonté de payer pour Bon App’ ni viabilité d’un abonnement ou de livres imprimés. | [Matrice concurrentielle](./matrice-concurrentielle.md), sources concurrentielles consultées le 05/11/2026 ; [spécification v2.1](./Document-de-spécifications-produit-v2.1.pptx), consultée le 06/11/2026. | **hypothèse** | Le modèle de revenus devra être testé séparément de la valeur produit ; les offres concurrentes ne permettent pas d’en déduire le prix ou la conversion attendue. | Établir coûts variables et marge des fonctions et de l’impression ; tester les paliers, la disposition à payer et les alternatives sans confondre intention déclarée et achat réel. |

## Menaces — facteurs externes

| # | Formulation | Source | Statut | Conséquence pour le projet | Vérification nécessaire |
|---|---|---|---|---|---|
| M1 | Plusieurs concurrents directs annoncent déjà l’import ou le scan de recettes, l’organisation et, pour certains, le partage ou la collaboration ; des offres gratuites et payantes sont également documentées. | [Matrice concurrentielle](./matrice-concurrentielle.md), sources officielles consultées le 05/11/2026. | **fait documenté** | Le recouvrement fonctionnel rendrait une proposition limitée à « sauvegarder et organiser des recettes » difficile à distinguer ; l’effet sur l’adoption de Bon App’ n’est pas mesuré. | Tester les offres concurrentes et comparer leurs résultats, leurs limites et leurs conditions ; vérifier auprès d’utilisateurs quels bénéfices influencent réellement leur choix. |
| M2 | **Hypothèse :** des outils généralistes déjà utilisés pour noter, partager des messages ou échanger des médias pourraient suffire à certaines personnes pour conserver ou transmettre des recettes, malgré l’absence de structure culinaire documentée dans les sources consultées. | [Matrice concurrentielle](./matrice-concurrentielle.md), notamment les sources Google Keep et WhatsApp consultées le 05/11/2026. | **hypothèse** | Un concurrent de substitution peut être une habitude ou un assemblage d’outils plutôt qu’une application culinaire ; le coût de changement pourrait réduire l’intérêt d’une application dédiée. | Interroger les personnes sur leurs solutions réelles, les échecs de recherche/transmission et les raisons de changer ou de conserver leurs outils actuels. |
| M3 | **Hypothèse :** les parcours reposant sur des services tiers et des capacités propres aux plateformes (OCR, stockage média, import depuis messagerie, notifications, impression) pourraient être limités par leur disponibilité, leurs coûts ou leurs conditions d’accès. Les choix correspondants ne sont pas tous arrêtés. | [Pile technique](../architecture/technology-stack.md) et [spécification v2.1](./Document-de-spécifications-produit-v2.1.pptx), consultées le 06/11/2026. | **hypothèse** | Une dépendance indisponible ou trop coûteuse pourrait retarder ou réduire une fonction centrale, ou produire une expérience inégale entre web, iOS et Android. | Confirmer les mécanismes officiellement disponibles par plateforme ; comparer coûts, conditions, régions et solutions de repli avant de faire dépendre le MVP d’un fournisseur. |

## Informations manquantes

Les éléments ci-dessous empêchent de tirer une conclusion plus ferme sur la viabilité ou la priorité des pistes :

- résultats d’entretiens, d’observations ou de tests utilisateurs, et validation des personas ;
- taille, évolution et segmentation du marché, ainsi que sources indépendantes sur les usages de recettes familiales ;
- comparaison en usage des concurrents : qualité d’import/OCR, facilité de partage, recherche, rétention et limites ;
- volonté de payer, coût d’acquisition, coûts d’exploitation, budget disponible et économie unitaire des offres ;
- responsables, échéancier et capacité de livraison du projet ; état réel des prototypes ou travaux hors des fichiers consultés ;
- décisions fournisseurs et critères de disponibilité, coût, localisation, rétention et conformité des données ;
- mesure de la demande réelle pour des fonctions de mémoire familiale par rapport aux fonctions utilitaires de cuisine.

## Contre-analyse

### Classements potentiellement discutables

- La clarté d’une vision est classée comme **force interne**, mais elle n’est ni une capacité produit réalisée ni un avantage concurrentiel prouvé. Elle peut aussi conduire à un biais de cadrage si les utilisateurs ne partagent pas cette priorité.
- L’absence d’implémentation et de recherche validée est classée comme **faiblesse interne**, car elle concerne l’état documenté du projet ; elle ne permet pas de conclure que l’équipe n’a réalisé aucun travail hors dépôt.
- Le recouvrement concurrentiel est classé comme **menace externe** ; il pourrait aussi signaler un marché et des usages existants. La matrice ne mesure ni les parts de marché ni l’intensité concurrentielle.
- Les risques de fournisseurs et de plateformes sont classés comme **menace externe** seulement en tant qu’effets possibles de contraintes extérieures. Le fait documenté est que les choix sont ouverts ; aucun incident, refus d’accès ou coût excessif n’est établi.

### Conclusions trop optimistes à éviter

- Ne pas présenter « mémoire familiale », « transmission intergénérationnelle » ou « simplicité pour tous les âges » comme besoins validés ou avantages acquis.
- Ne pas transformer les cibles de moins de 10 secondes, de fréquence d’usage ou d’enrichissement en résultats, prévisions ou preuves d’adoption.
- Ne pas déduire une place de marché inoccupée : plusieurs comparables documentent déjà des recettes familiales, des collections partagées, de la collaboration ou de la numérisation.
- Ne pas supposer que le modèle freemium, l’abonnement ou l’impression sera rentable parce que des offres comparables existent.
- Ne pas traiter une architecture cible ou une fonction prévue comme déjà disponible, faisable dans le budget ou cohérente sur les trois plateformes.

### Hypothèses prioritaires à tester

1. **Problème et comportement :** les familles ont-elles une difficulté fréquente et suffisamment importante à retrouver ou transmettre des recettes, au-delà de la situation décrite dans la vision ?
2. **Valeur distinctive :** les auteurs, variantes et anecdotes augmentent-ils l’usage ou la transmission par rapport à une bonne fonction de scan, de recherche et de partage ?
3. **Faisabilité et confiance :** peut-on capturer une recette sur photo avec une qualité, un temps de correction et une expérience intergénérationnelle acceptables, tout en respectant la confidentialité et les limites des plateformes ?
4. **Viabilité économique :** quelles fonctions, le cas échéant, les utilisateurs paieraient-ils, et les revenus couvriraient-ils les coûts d’OCR, de stockage, de synchronisation et de support ?
