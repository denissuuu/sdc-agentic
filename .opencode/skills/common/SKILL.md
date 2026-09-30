---
name: common
description: Règles communes de sobriété en tokens et de qualité de code partagées par toute l'équipe (orchestrateur, dev, testeur). À charger avant toute tâche de développement, de test ou d'orchestration dans ce projet.
---

# Règles communes

## Sobriété en tokens

- Résumer plutôt que copier ; chaque réponse aussi courte que possible.
- Utiliser grep/glob ciblés avant de lire un fichier entier.
- Un seul passage de modification : lire une fois, éditer, ne pas revenir 3 fois.
- Ne pas imprimer de gros fichiers (logs, package-lock, node_modules) dans le contexte.
- Ne pas dupliquer le travail d'un autre agent ; se fier aux rapports.
- Ne pas relancer une commande lourde si un résultat déjà remonté suffit.
- Ne pas relire un fichier déjà couvert par un rapport de sous-agent : le rapport est la version courte et vérifiée.
- Regrouper les lectures et les vérifications proches en une seule commande plutôt que d'enchaîner les appels.
- Poser une question fermée plutôt que trois options à commenter.
- Ne pas coller un diff ni un rapport complet quand trois lignes suffisent.

## Qualité du code

- Respecter les conventions existantes du projet (langage, structure, nommage).
- Aucun commentaire de code sauf demande explicite.
- Ne jamais commiter, sauvegarder ou dévoiler des secrets/clés.
- Nettoyer son propre désordre : pas de fichiers temporaires inutiles.
- Remonter tout doute sur la demande au lieu de deviner.
- Un changement hors périmètre se signale, il ne s'ajoute pas d'office.

## Secrets

- Aucun secret dans un fichier, un commit, un log ou un rapport : ni clé, ni token, ni mot de passe, ni identifiant, ni variable sensible.
- `.env` et ses variantes restent ignorés par `.gitignore` ; seul un `.env.example` sans valeur est admis.
- Une valeur aperçue dans un fichier se signale par son chemin et sa ligne, elle ne se recopie jamais dans le rapport.
- Ne pas exécuter une commande qui affiche des variables d'environnement ou des fichiers de credentials.
- Au moindre doute sur le caractère sensible d'une valeur, traite-la comme un secret.

## Équipe

- `orchestrator` planifie et délègue (jamais de code ni de tests).
- `dev` implémente, refactore, corrige.
- `tester` exécute les tests et valide.
- Flux : orchestrateur → dev → tester → synthèse.