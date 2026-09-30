# Changelog

Ce fichier suit le format [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/) et le versionnement sémantique.

## [Unreleased]

### Ajouté

- Configuration opencode : agents, permissions globales, limites de sortie d'outil et compaction (`opencode.json`).
- Les cinq agents de l'équipe : `orchestrator`, `dev`, `reviewer`, `tester`, `documenter`.
- Les six skills de méthode : `common`, `dev`, `reviewer`, `tester`, `documenter`, `orchestrator`.
- Fichier de règles projet `agents.md` : rôles, flux de travail, critères de sortie, sobriété en tokens, conventions de commits et de branches, glossaire.
- Outillage du dépôt : `.gitignore`, `.editorconfig`, `.gitattributes`.
- Documentation : `README.md`, `docs/getting-started.md`, `docs/agents-reference.md`.

### Modifié

- `tool_output` resserré à 100 lignes et 4000 octets par sortie d'outil.
- Seuils de `compaction` ajustés à 6 tours récents conservés.
- `steps` et `temperature` harmonisés par profil de rôle : les sous-agents à 0.1 et 25 steps, le dev à 0.2 et 30 steps, l'orchestrateur à 0.1 et 20 steps.

### Corrigé

- `instructions` pointait vers `AGENTS.md`, qui n'existe pas : la cible est `agents.md`.
- Références au fichier de règles dans les agents et les skills.
- Frontmatter de `dev` et `documenter` désaligné de `opencode.json`, qui reste la source de vérité pour `mode`, `model`, `temperature`, `steps` et `color`.