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

## Qualité du code

- Respecter les conventions existantes du projet (langage, structure, nommage).
- Aucun commentaire de code sauf demande explicite.
- Ne jamais commiter, sauvegarder ou dévoiler des secrets/clés.
- Nettoyer son propre désordre : pas de fichiers temporaires inutiles.
- Remonter tout doute sur la demande au lieu de deviner.

## Équipe

- `orchestrator` planifie et délègue (jamais de code ni de tests).
- `dev` implémente, refactore, corrige.
- `tester` exécute les tests et valide.
- Flux : orchestrateur → dev → tester → synthèse.