# Changelog

## 2.0.1 — 2026-09-05

- Corrige un `RecursionError` dans le moteur anti-chevauchement du replayer.
- Le placement des sièges hors des zones board/pot/action est désormais borné et strictement itératif.
- Ajoute un test de régression pour empêcher le retour de cette récursion.

## 2.0.0

### Added
- warehouse analytique incrémental `hero_hand_fact` ;
- onglet Rapports avancés ;
- rapports position, limite, starting hand, type de pot, ligne préflop, jour, street actions, adversaires ;
- Leak Finder conservateur ;
- mini-langage de filtres ;
- filtres sauvegardés ;
- export CSV ;
- heatmap 13×13 Hero ;
- tags de mains ;
- notes joueurs ;
- onglet Outils DB ;
- backup SQLite en ligne, integrity check, optimize, vacuum ;
- tests pytest pour reports/query/backup ;
- documentation de parité fonctionnelle.

### Preserved
- parser/replayer/range/EV de la 1.0 avec leurs tests de régression ;
- garde-fou review-only.

## 1.0.0
- première base GitHub stable issue des versions 0.9.x.
