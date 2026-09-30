# Règles du projet (tous les agents)

Ce fichier s'applique à l'orchestrateur, au dev, au reviewer, au testeur et au documenter. Le lire en entier au début de chaque session.

## Équipe et rôles

- **orchestrator** : planifie et délègue. Ne fait jamais de code ni de tests lui-même.
- **dev** : implémente, refactore, corrige le code et les fichiers.
- **reviewer** : relit le travail du dev, vérifie qualité, conventions, sécurité et cas limites, remonte un rapport PASS/FAIL.
- **tester** : exécute les tests, valide le travail du dev, remonte les échecs.
- **documenter** : génère ou met à jour README, docs et changelog, uniquement sur demande explicite.

## Flux de travail

Toute demande utilisateur est traitée par l'orchestrateur, qui délègue au sous-agent le plus pertinent puis synthétise.

Flux standard :

1. `orchestrator` analyse la demande et la découpe en tâches.
2. `orchestrator` délègue l'implémentation au `dev`.
3. `orchestrator` délègue la revue du travail du `dev` au `reviewer`.
4. `orchestrator` délègue la validation au `tester`.
5. `orchestrator` synthétise le résultat pour l'utilisateur.

Boucle de correction : si le `reviewer` remonte des points bloquants ou si le `tester` remonte des échecs, l'orchestrateur redélègue la correction au `dev`, puis re-valide (revue et/ou tests) avant de synthétiser.

Variantes :

- Documentation seule : `orchestrator` → `documenter` → synthèse, sans `dev` ni `tester`.
- Correction simple et vérifiable : `orchestrator` → `dev` → `tester` → synthèse, la revue peut être sautée.
- Revue d'un travail existant : `orchestrator` → `reviewer` → synthèse, puis `dev` uniquement si le verdict est FAIL.

## Critères de sortie par rôle

Un agent a terminé quand il produit la preuve attendue, pas seulement une intention.

- **orchestrator** : synthèse courte pour l'utilisateur (résultat, statut, reste à faire) et plan `todowrite` à jour.
- **dev** : modification faite en place, rapport listant les fichiers touchés et les vérifications réellement exécutées avec leur résultat.
- **reviewer** : rapport avec statut PASS ou FAIL ; un FAIL sans liste de points bloquants est incomplet.
- **tester** : rapport avec statut PASS ou FAIL et les commandes réellement exécutées ; aucune commande inventée.
- **documenter** : liste des fichiers créés ou modifiés, cohérents avec l'état réel du dépôt.

Aucun agent ne déclare une tâche terminée sans avoir exécuté la vérification qui lui incombe.

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

Voir le fichier `agents.md` (racine). Toute incompréhension de la demande doit être remontée à l'orchestrateur.