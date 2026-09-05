# Poker Review Lab 2.1

Poker Review Lab est une application **post-session** de tracking, review et analyse d'historiques de mains, développée d'abord pour Winamax. La v2.1 consolide le prototype 0.9.x / 1.0 en un projet beaucoup plus proche d'un vrai tracker de bureau : rapports persistants, warehouse analytique, filtres avancés, tags, notes joueurs, sauvegardes, CI et build Windows.

> **Portée volontaire :** analyse après session uniquement. Les fonctions d'analyse exploit/GTO restent verrouillées lorsqu'une room connue est détectée. Le projet ne cherche pas à fournir un HUD décisionnel temps réel.

## Ce que contient la v2.0

### Tracking et base
- import/déduplication Winamax et support PokerStars hérité ;
- SQLite WAL + index analytiques ;
- cache `hand_analytics` pour Net, BB, gros pots, showdown, all-in, tags de review ;
- nouveau **warehouse `hero_hand_fact`** dénormalisé et incrémental pour accélérer les rapports ;
- sauvegarde SQLite en ligne, `integrity_check`, `foreign_key_check`, `ANALYZE`, `PRAGMA optimize`, VACUUM ;
- migrations non destructives des tables de rapports/tags/notes.

### Rapports avancés
- vue générale ;
- par position ;
- par limite ;
- par main de départ ;
- par type de pot ;
- par ligne préflop ;
- par jour ;
- actions Hero par street ;
- adversaires ;
- **Leak Finder conservateur** basé sur la comparaison interne et la taille d'échantillon ;
- export CSV ;
- filtres sauvegardés ;
- filtre visuel + mini-langage de requête ;
- heatmap 13×13 des résultats des mains de départ.

Exemples du mini-langage :

```text
position=BTN and pot>=20
stake=NL10 and net<0
showdown=true and hand~AK
type=3BET and tag=Bluff
date>=2026-01-01
```

### Interface de review 2.1
- état du replayer unique et synchronisé avec les animations ;
- rail fixe HERO | BOARD | VILAIN comme référence visuelle ;
- range avant/après avec value / showdown / draw / air ;
- explication textuelle de ce que chaque carte/action change ;
- Coach en choix robuste avec équité en plage et fiabilité explicite ;
- mode simple par défaut, mode expert à la demande ;
- outils avancés regroupés dans `Analyse ▾` en mode simple pour libérer de la hauteur ;
- table visuellement moins dominante pour privilégier board, range et décision ;
- timeline inférieure masquable pour maximiser l’espace.

### Review
- replayer street par street ;
- stacks et pot dynamiques ;
- animations ;
- cartes Hero / board / Villain visibles ensemble ;
- range adverse live combo par combo avec blockers et repondération selon actions/sizings ;
- Coach Exploit contextuel comparant les actions légales et plusieurs sizings ;
- incertitude statistique explicite ;
- import de références GTO externes authentiques ;
- aucune stratégie GTO inventée en l'absence de source.

### Organisation du travail
- tags de mains ;
- notes personnelles sur les joueurs ;
- profils HUD post-session ;
- file de mains à revoir ;
- sessions automatiques ;
- gros gains / grosses pertes / gros pots ;
- filtres persistants.

## Installation rapide

Python 3.11+ avec Tkinter :

```bash
python poker_review_lab.py
```

Sous Windows, `run_windows.bat` lance l'application.

## Tests

```bash
python self_test.py
python -m pytest -q
```

La CI teste Python 3.11, 3.12 et 3.13, compile les modules, exécute les régressions poker et les tests du warehouse/filtrage.

## Architecture

```text
Poker-Review-Lab/
├─ poker_review_lab.py       # application UI + moteurs historiques hérités
├─ prl_core/
│  ├─ reports.py             # warehouse, rapports, tags, notes, filtres
│  ├─ query.py               # mini-langage de filtres auditable
│  └─ dbtools.py             # backup, intégrité, optimisation
├─ tests/                    # tests pytest supplémentaires
├─ docs/                     # maths, architecture, matrice de fonctionnalités
├─ examples/                 # HH et schéma GTO d'exemple
└─ .github/workflows/        # tests, build Windows, release
```

Le gros module historique reste présent pour préserver les nombreuses régressions du parser/replayer/EV. Les nouveaux sous-systèmes de production sont désormais extraits dans `prl_core`, et les futures modifications peuvent continuer cette séparation sans casser la compatibilité.

## PT4 / HM3 : objectif réaliste

Poker Review Lab 2.0 reprend plusieurs idées de produits matures — rapports interactifs, filtres sauvegardés, hand heatmaps, tagging, notes, replayer, range visualizer, leak review — mais **n'est pas présenté comme étant déjà à parité fonctionnelle avec PokerTracker 4 ou Holdem Manager 3**. Voir `docs/FEATURE_MATRIX.md`.

Le HUD temps réel de PT4/HM3 n'est volontairement pas reproduit dans cette branche : le projet reste centré sur la review après session.

## Releases GitHub

`release_request.json` pilote le workflow de Release. Une modification de version sur `main` déclenche les tests puis crée un tag et un package de release.

## Données utilisateur

La base principale reste dans :

```text
~/.poker_review_lab/
```

Elle n'est jamais versionnée dans Git.
