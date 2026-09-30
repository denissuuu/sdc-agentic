# Démarrage

Ce dépôt contient une équipe d'agents opencode prêts à l'emploi, pensés pour travailler en français : un orchestrateur qui découpe et délègue, un développeur, un reviewer, un testeur et un documenter. Le code n'y vit pas encore : tout est configuration, règles et documentation.

## Prérequis

- opencode installé et lancé sur ce dossier.
- Rien à installer dans le dépôt : aucune dépendance, aucun build, aucun test automatique.

## Structure du dépôt

```
.
├── .opencode/
│   ├── agent/     # orchestrator, dev, reviewer, tester, documenter
│   └── skills/    # common, dev, reviewer, tester, documenter, orchestrator
├── docs/
│   ├── agents-reference.md   # rôle et paramètres de chaque agent
│   └── getting-started.md    # ce fichier
├── .editorconfig
├── .gitattributes
├── .gitignore
├── CHANGELOG.md
├── README.md
├── agents.md      # règles projet, lues dans toutes les sessions
└── opencode.json  # configuration opencode
```

## Comment opencode charge les agents et les skills

- `opencode.json` déclare les cinq agents dans la clé `agent`, avec leur `mode`, leur `model`, leur `temperature`, leurs `steps`, leur `color` et leurs permissions. C'est la source de vérité.
- `opencode.json` déclare aussi `instructions` : le fichier `agents.md` est chargé automatiquement dans chaque session, avant toute tâche.
- Chaque agent est décrit dans `.opencode/agent/<nom>.md`. Son frontmatter doit rester cohérent avec `opencode.json`.
- Les skills sont des méthodes rangées dans `.opencode/skills/<nom>/SKILL.md`. Ils ne sont pas appliqués automatiquement : chaque agent les charge au besoin avec l'outil `skill`, puis applique la méthode.

## Lancer un agent

- L'agent par défaut est `orchestrator` (`default_agent`). Une demande passe donc par lui, qui délègue ensuite avec l'outil `task`.
- Pour cibler un rôle, nomme-le dans la demande : il sera alors traité en direct plutôt que délégué.
- `dev` est un agent principal (`mode: all`), `orchestrator` est l'agent principal de l'équipe (`mode: primary`), les trois autres sont des sous-agents (`mode: subagent`) : ils ne s'appellent pas entre eux, seule l'équipe ne délègue qu'aux quatre rôles autorisés.

## Workflow

Le flux standard, décrit dans `agents.md` :

1. `orchestrator` analyse la demande et la découpe en tâches.
2. `orchestrator` délègue l'implémentation au `dev`.
3. `orchestrator` délègue la revue au `reviewer`.
4. `orchestrator` délègue la validation au `tester`.
5. `orchestrator` synthétise le résultat.

Si le `reviewer` ou le `tester` renvoie un `FAIL`, l'orchestrateur redélègue la correction au `dev`, puis re-valide. La documentation est traitée à part par le `documenter`, uniquement sur demande explicite.

## Où lire les règles

- `agents.md` : rôles, flux de travail, critères de sortie par rôle, sobriété en tokens, qualité du code, conventions de commits et de branches, glossaire.
- `docs/agents-reference.md` : rôle et paramètres de chaque agent, ses permissions et ses limites.
- `CHANGELOG.md` : ce qui a changé et pourquoi.