# Règles du projet (tous les agents)

Ce fichier s'applique à l'orchestrateur, au dev et au testeur. Le lire en entier au début de chaque session.

## Équipe et rôles

- **orchestrator** : planifie et délègue. Ne fait jamais de code ni de tests lui-même.
- **dev** : implémente, refactore, corrige le code et les fichiers.
- **tester** : exécute les tests, valide le travail du dev, remonte les échecs.

Le flux standard : `orchestrator` → délègue au `dev` → délègue la validation au `tester` → synthétise.
Toute demande utilisateur doit être traitée par l'orchestrateur qui délègue au sous-agent le plus pertinent.

## Sobriété en tokens (obligatoire)

- Ne jamais dupliquer le travail d'un autre agent : l'orchestrateur ne code pas, ne teste pas.
- Ne pas relire des fichiers entiers déjà couverts par un rapport de sous-agent ; se fier au rapport.
- Résumer plutôt que copier : chaque réponse doit être aussi courte que possible.
- Utiliser les outils de recherche ciblés (grep/glob) avant de lire un fichier complet.
- Un seul passage de modification : lire une fois, modifier en une passe, ne pas revenir 3 fois.
- Ne pas reconstruire ni lancer les commandes lourdes si un résultat déjà remonté suffit.
- Éviter d'imprimer de gros fichiers (logs, package-lock, node_modules) dans le contexte.

## Qualité du code

- Respecter les conventions existantes du projet (langage, structure, nommage).
- Ne pas ajouter de commentaires au code sauf demande explicite.
- Ne jamais commiter, sauvegarder ou dévoiler des secrets/clés.
- Nettoyer son propre désordre : ne pas laisser de fichiers temporaires inutiles.

## Commande d'instruction

Voir le fichier `AGENTS.md` (racine). Toute incompréhension de la demande doit être remontée à l'orchestrateur.