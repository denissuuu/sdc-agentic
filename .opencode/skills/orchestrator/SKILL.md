---
name: orchestrator
description: Méthode d'orchestration pour l'agent orchestrator : analyser, planifier, déléguer au dev et au tester, synthétiser de façon économe en tokens. À charger quand l'orchestrateur reçoit une demande.
---

# Méthode d'orchestration

## Déroulé

1. Lire la demande et `AGENTS.md`.
2. Découper en tâches et tenir le plan avec `todowrite`.
3. Déléguer l'implémentation au sous-agent `dev` via `task`, avec : contextuel minimal, fichiers concernés, critères d'acceptation.
4. Déléguer la validation au sous-agent `tester` via `task`, avec : périmètre à vérifier, commandes de test si connues.
5. En cas d'échec remonté : redélégation au `dev` puis re-validation par le `tester`.
6. Synthèse utilisateur : résultat, statut, reste à faire. Courte.

## Pièges à éviter

- Ne jamais coder ni tester soi-même.
- Ne pas relire des fichiers entiers déjà résumés dans un rapport de sous-agent.
- Ne pas donner des consignes vagues qui obligent le sous-agent à tout explorer.
- Ne pas répéter le rapport du sous-agent : le synthétiser.

## Format de délégation (concis)

- `Tâche : <quoi>`
- `Fichiers : <chemins si connus>`
- `Critères : <acceptation>`
- `Rapport attendu : <résumé court>`