# Référence des agents

Les valeurs de cette page sont celles de `opencode.json`, qui reste la source de vérité. Les fichiers `.opencode/agent/<nom>.md` ne doivent jamais le contredire.

## Configuration globale

| Réglage | Valeur |
| --- | --- |
| `model` | `opencode/big-pickle` |
| `small_model` | `opencode/big-pickle` |
| `default_agent` | `orchestrator` |
| `instructions` | `agents.md` |
| `tool_output.max_lines` | 100 |
| `tool_output.max_bytes` | 4000 |
| `compaction.auto` | `true` |
| `compaction.tail_turns` | 6 |

Les permissions globales (`read`, `edit`, `glob`, `grep`, `list`, `bash`, `task`, `external_directory`, `todowrite`, `webfetch`, `websearch`, `lsp`, `skill`, `question`) sont toutes en `allow`. Chaque agent peut les restreindre : c'est le cas de `task`.

## orchestrator

- **Rôle** : analyse la demande, la découpe, délègue au bon sous-agent et synthétise le résultat.
- **Fichier** : `.opencode/agent/orchestrator.md`

| Paramètre | Valeur |
| --- | --- |
| `mode` | `primary` |
| `model` | `opencode/big-pickle` |
| `temperature` | 0.1 |
| `steps` | 20 |
| `color` | `primary` |

- **Permissions `task`** : `dev`, `reviewer`, `tester` et `documenter` en `allow`, tout le reste en `deny`.
- **Peut** : découper une demande, tenir un plan avec `todowrite`, déléguer via `task`, arbitrer les verdicts, synthétiser.
- **Ne peut pas** : écrire ou modifier du code, exécuter des tests, corriger à la place d'un sous-agent.

## dev

- **Rôle** : implémente, refactore et corrige le code et les fichiers.
- **Fichier** : `.opencode/agent/dev.md`

| Paramètre | Valeur |
| --- | --- |
| `mode` | `all` |
| `model` | `opencode/big-pickle` |
| `temperature` | 0.2 |
| `steps` | 30 |
| `color` | `success` |

- **Permissions `task`** : tout en `deny`, aucun sous-agent appelable.
- **Peut** : lire, chercher, modifier des fichiers, exécuter des commandes de vérification, rapporter les changements.
- **Ne peut pas** : déléguer à un autre agent, commiter, pousser, ou imposer un choix quand la demande est ambiguë.

## reviewer

- **Rôle** : relit le travail du dev et remonte un rapport `PASS` ou `FAIL`.
- **Fichier** : `.opencode/agent/reviewer.md`

| Paramètre | Valeur |
| --- | --- |
| `mode` | `subagent` |
| `model` | `opencode/big-pickle` |
| `temperature` | 0.1 |
| `steps` | 25 |
| `color` | `info` |

- **Permissions `task`** : tout en `deny`, aucun sous-agent appelable.
- **Peut** : relire les fichiers concernés du changement, vérifier conventions, sécurité et cas limites, signaler des points bloquants.
- **Ne peut pas** : corriger le code lui-même, ni commiter. Toute correction passe par le `dev`.

## tester

- **Rôle** : exécute les tests, valide le travail du dev et remonte les échecs.
- **Fichier** : `.opencode/agent/tester.md`

| Paramètre | Valeur |
| --- | --- |
| `mode` | `subagent` |
| `model` | `opencode/big-pickle` |
| `temperature` | 0.1 |
| `steps` | 25 |
| `color` | `warning` |

- **Permissions `task`** : tout en `deny`, aucun sous-agent appelable.
- **Peut** : lancer les commandes de test réellement définies dans le dépôt, tester les cas limites, remonter un rapport d'escalade.
- **Ne peut pas** : inventer une commande de test, corriger le code, ni valider un changement qu'il n'a pas exécuté.

## documenter

- **Rôle** : génère ou met à jour README, documentation et changelog, uniquement sur demande explicite.
- **Fichier** : `.opencode/agent/documenter.md`

| Paramètre | Valeur |
| --- | --- |
| `mode` | `subagent` |
| `model` | `opencode/big-pickle` |
| `temperature` | 0.1 |
| `steps` | 25 |
| `color` | `muted` |

- **Permissions `task`** : tout en `deny`, aucun sous-agent appelable.
- **Peut** : créer ou modifier les documents explicitement demandés, en respectant le style et la langue existants.
- **Ne peut pas** : créer un fichier `.md` non demandé, inventer une fonctionnalité ou un élément de licence, ni commiter.

## Tableau récapitulatif

| Agent | `mode` | `model` | `temperature` | `steps` | `color` | `task` |
| --- | --- | --- | --- | --- | --- | --- |
| `orchestrator` | `primary` | `opencode/big-pickle` | 0.1 | 20 | `primary` | délègue aux 4 rôles |
| `dev` | `all` | `opencode/big-pickle` | 0.2 | 30 | `success` | tout `deny` |
| `reviewer` | `subagent` | `opencode/big-pickle` | 0.1 | 25 | `info` | tout `deny` |
| `tester` | `subagent` | `opencode/big-pickle` | 0.1 | 25 | `warning` | tout `deny` |
| `documenter` | `subagent` | `opencode/big-pickle` | 0.1 | 25 | `muted` | tout `deny` |