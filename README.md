# Équipe d'agents opencode

Un dépôt de configuration qui définit une équipe d'agents opencode en français : un orchestrateur qui découpe et délègue, un développeur, un reviewer, un testeur et un documenter. Il n'y a pas de code applicatif ici, uniquement des règles, des paramètres et de la documentation.

## Pourquoi

- Chaque rôle a un périmètre net : celui qui écrit ne valide pas, celui qui valide ne corrige pas.
- Le flux est standardisé : `orchestrator` → `dev` → `reviewer` → `tester`, avec boucle de correction sur `FAIL`.
- Les règles du projet sont versionnées avec la configuration et injectées dans chaque session.
- Les skills décrivent des méthodes précises, pas des intentions : elles sont appliquées à chaque fois.

## Arborescence

```
.
├── .opencode/
│   ├── agent/     # orchestrator, dev, reviewer, tester, documenter
│   └── skills/    # common, dev, reviewer, tester, documenter, orchestrator
├── docs/
│   ├── agents-reference.md   # rôle et paramètres de chaque agent
│   └── getting-started.md    # guide de démarrage
├── .editorconfig
├── .gitattributes
├── .gitignore
├── CHANGELOG.md
├── README.md
├── agents.md      # règles projet, chargées dans toutes les sessions
└── opencode.json  # configuration opencode, source de vérité
```

## Agents

| Agent | Rôle | `mode` | `steps` |
| --- | --- | --- | --- |
| `orchestrator` | Planifie, délègue, synthétise | `primary` | 20 |
| `dev` | Implémente, refactore, corrige | `all` | 30 |
| `reviewer` | Relit et rend un verdict `PASS`/`FAIL` | `subagent` | 25 |
| `tester` | Exécute les tests et valide | `subagent` | 25 |
| `documenter` | Rédige la documentation, sur demande | `subagent` | 25 |

Détail des paramètres et des permissions : [`docs/agents-reference.md`](docs/agents-reference.md).

## Skills

| Skill | Méthode qu'elle apporte |
| --- | --- |
| `common` | Sobriété en tokens, qualité du code, gestion des secrets |
| `orchestrator` | Analyser, planifier, déléguer, arbitrer, synthétiser |
| `dev` | Comprendre, écrire en un passage, vérifier, rapporter |
| `reviewer` | Conventions, sécurité, cas limites, rapport `PASS`/`FAIL` |
| `tester` | Commandes réelles, cas limites, rapport d'escalade |
| `documenter` | Ne rien écrire sans demande, style documentaire |

## Usage

- Ouvrir le dossier dans opencode : `opencode.json` et `agents.md` sont chargés automatiquement.
- Écrire la demande en langage naturel : elle est traitée par `orchestrator`, qui découpe et délègue.
- Nommer un rôle dans la demande pour l'implémenter directement, par exemple « relis ce diff en tant que reviewer ».
- Le détail du chargement des agents, du lancement et du workflow est dans [`docs/getting-started.md`](docs/getting-started.md).

## Contribution

- Commencer par lire [`agents.md`](agents.md) : rôles, flux de travail, critères de sortie, sobriété en tokens, conventions de commits et de branches.
- Suivre [`docs/getting-started.md`](docs/getting-started.md) pour le fonctionnement d'opencode sur ce dépôt.
- `opencode.json` est la source de vérité : toute modification doit rester cohérente avec le frontmatter de `.opencode/agent/*.md`.
- Un changement logique par commit, message en Conventional Commits et en français.
- Aucun agent ne pousse et ne réécrit l'historique : cela relève de vous.

## Documentation

- [`agents.md`](agents.md) : règles du projet.
- [`docs/getting-started.md`](docs/getting-started.md) : démarrage et workflow.
- [`docs/agents-reference.md`](docs/agents-reference.md) : référence des agents.
- [`CHANGELOG.md`](CHANGELOG.md) : ce qui a changé.