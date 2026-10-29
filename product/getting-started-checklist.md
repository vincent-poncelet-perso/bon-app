# Checklist de démarrage — Bon App’

Cette checklist décrit ce qu’une personne découvrant le dépôt peut consulter et faire à partir
des fichiers présents. Elle distingue les documents et dossiers existants des technologies et
fonctionnalités seulement envisagées.

## Documents de référence à consulter

- [README](../README.md) — présente les grandes rubriques du dépôt.
- [Vision produit](./vision.md) — décrit le problème, les utilisateurs visés, la promesse et les
  objectifs du MVP.
- [Spécification produit v2.1](./Document-de-spécifications-produit-v2.1.pptx) — détaille les
  besoins et parcours envisagés.
- [Pile technique](../architecture/technology-stack.md) — expose les technologies cibles et les
  décisions techniques encore ouvertes.
- [Règles d’architecture](../architecture/architecture-rules.md) — décrit les frontières et
  responsabilités prévues pour les composants.
- [Conventions de développement](../architecture/coding-conventions.md) — définit les
  conventions à appliquer lorsque le code sera créé.
- [Règles de sécurité](../security/security-rules.md) — décrit les exigences de sécurité
  prévues.
- [Definition of Done](./definition-of-done.md) — définit les critères envisagés pour considérer
  un changement terminé.

## Prérequis confirmés par le dépôt

- **Présent :** documentation Markdown et spécification produit PowerPoint.
- **Présent :** répertoires réservés aux applications, aux packages et aux tests, actuellement
  sans implémentation.
- **Non confirmé :** aucun prérequis logiciel de développement n’est établi par un manifeste,
  une configuration d’installation ou une procédure de démarrage dans le dépôt.
- **Non installé ou configuré d’après les fichiers suivis :** les technologies citées dans la
  pile technique sont des cibles documentées, et non des dépendances attestées par des manifestes
  ou un lockfile.

## Étapes disponibles aujourd’hui

- [ ] Lire les documents de référence ci-dessus pour comprendre le produit et les choix envisagés.
- [ ] Parcourir les répertoires existants pour distinguer les zones documentées des emplacements
  encore vides.
- [ ] Traiter les technologies et fonctionnalités présentées comme des cibles comme des intentions,
  sauf lorsqu’une implémentation ou une configuration correspondante est ajoutée au dépôt.

**Aucun parcours de lancement ou d’exécution des tests n’est documenté à ce stade.** Le dépôt ne
fournit pas de commande d’installation, de démarrage, de build ou de test à exécuter.

## Éléments restant à définir

- Créer les manifestes, configurations et scripts nécessaires avant de pouvoir installer,
  démarrer, construire ou tester les applications.
- Verrouiller les versions et ajouter les configurations de dépendances correspondantes.
- Définir les commandes de démarrage et de test, puis les documenter une fois qu’elles sont
  réellement disponibles.
- Configurer la CI et les contrôles automatisés.
- Trancher les décisions techniques et opérationnelles encore ouvertes dans la
  [pile technique](../architecture/technology-stack.md), notamment les fournisseurs, les
  environnements et l’hébergement.
