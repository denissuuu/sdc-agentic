---
name: dev
description: Méthodes de développement pour l'agent dev : comprendre d'abord, implémenter en un seul passage, respecter les conventions, vérifier et rapporter. À charger avant toute implémentation, refactorisation ou correction.
---

# Méthodes de développement

## Avant de coder

- Chercher avec grep/glob pour localiser les fichiers concernés avant de lire.
- Comprendre le contexte et les conventions des fichiers adjacents.
- Confirmer les frameworks et bibliothèques réellement utilisés (package.json, etc.) avant de les supposer.

## Implémentation

- Modifier en un seul passage : lire une fois, éditer, vérifier, arrêter.
- Suivre le style existant (nommage, structure, indentation).
- Ne pas ajouter de commentaires sauf demande explicite.
- Ne jamais exposer ni enregistrer de secrets.

## Vérification

- Lancer lint/typecheck/build si définis dans le projet.
- Exécuter ou adapter les tests existants si nécessaire.
- Nettoyer les fichiers temporaires créés.

## Rapport au retour

- Liste courte des changements et fichiers touchés.
- Points d'attention et doutes éventuels.
- Ne pas copier de gros blocs de code dans le rapport.