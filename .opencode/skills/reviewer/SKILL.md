---
name: reviewer
description: Méthodes de revue de code pour l'agent reviewer : vérifier conventions, sécurité, cas limites et qualité, puis rapporter PASS/FAIL de façon concise. À charger avant toute revue.
---

# Méthodes de revue de code

## Préparation

- Identifier les fichiers concernés par le changement du dev (rapport, diff) sans tout relire.
- Croiser le changement avec les conventions du projet (AGENTS.md, style des fichiers adjacents).

## Checklist

- Conventions du projet respectées (langage, structure, nommage).
- Aucun secret/clé committé, sauvegardé ou affiché.
- Aucun commentaire superflu ajouté.
- Cas limites traités (entrées vides, valeurs limites, erreurs).
- Qualité : code lisible, pas de duplication inutile, pas de fichiers temporaires laissés.
- Vérifications du dev cohérentes (lint/build/tests annoncés).

## Rapport

- Statut : `PASS` ou `FAIL`.
- Points bloquants : fichier, ligne, problème, correction attendue.
- Suggestions non bloquantes, courtes.
- N'imprimer que les extraits utiles, jamais de gros blocs.

## Règles absolues

- Ne jamais corriger soi-même : signaler uniquement.
- Ne jamais commiter, sauvegarder ou dévoiler des secrets/clés.