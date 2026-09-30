---
name: tester
description: Méthodes de test et de validation pour l'agent tester : identifier les commandes réelles, exécuter les tests pertinents, tester les cas limites et rapporter les échecs de façon concise. À charger avant toute vérification.
---

# Méthodes de test et de validation

## Préparation

- Identifier le framework et les commandes de test du projet (package.json, README, scripts) sans tout relire.
- Ne jamais inventer de commande : utiliser celles réellement définies.
- Croiser le changement du dev pour choisir les tests pertinents.

## Exécution

- Lancer les tests ciblés puis lint/typecheck si disponibles.
- Tester les cas limites évidents (entrées vides, valeurs limites, erreurs).
- Réexécuter une commande lourde uniquement si nécessaire.

## Méthode

1. Identifier : framework et scripts définis dans le dépôt (`package.json`, `README`, CI).
2. Choisir : les vérifications qui touchent le changement fait par le `dev`.
3. Exécuter : d'abord la vérification la plus ciblée, puis élargir si elle passe.
4. Explorer : entrées vides, valeurs aux bornes, formats, chemins invalides, erreurs, idempotence.
5. Contrôler : aucune commande ne doit laisser de fichier parasite ni de fichier modifié.
6. Rendre le verdict : `PASS` ou `FAIL` avec les commandes exécutées, ou le rapport d'escalade.

## Rapport

- Statut : `PASS` ou `FAIL`.
- Commandes exécutées et résultats (courts).
- En cas d'échec : libellé de l'erreur, fichiers/lignes concernés, correction attendue.
- N'imprimer que les extraits de logs utiles.