# Changelog

## 2.1.0 — 2026-09-05

- Synchronise strictement table, board, rail de cartes, range et Coach pendant les animations : aucun panneau ne prend de l’avance sur le replayer.
- Refond le Coach en **choix robuste** compréhensible : la moyenne, la borne prudente et l’incertitude ne se contredisent plus visuellement.
- Masque `P(best)` en mode simple et le renomme explicitement en mode expert.
- Réduit la fausse précision quand la fiabilité est faible et affiche une plage d’équité.
- Corrige le bug `risk_bb` lors de la déduplication d’un sizing ALL-IN.
- N’expose plus les erreurs Python internes dans l’interface normale.
- Ajoute une range **avant → après** à chaque action/carte avec résumé des combos effectifs et des classes qui montent/baissent.
- Ajoute une coloration sémantique de range : value / showdown / draw / air, survol des cellules et bordure de changement.
- Le rail HERO | BOARD | VILAIN devient la source principale des cartes en mode simple ; les cartes de sièges reviennent en mode expert.
- Ajoute un mode simple/expert et un bouton pour masquer/afficher la timeline inférieure.
- Condense les outils avancés dans un menu `Analyse ▾` en mode simple ; la barre complète ne réapparaît qu’en mode expert.
- Rend le tapis visuellement plus discret afin que board, range, action et recommandation dominent la lecture.
- Remplace l’indicateur principal `5/14` par un état lisible (`À TOI`, action, pot, montant à payer) ; le compteur reste secondaire.
- Agrandit les montants de mises engagées et donne plus d’espace à la range live.
- Remplace le panneau bas par une narration en six étapes : ce qui vient d’arriver, impact sur la range, état Hero, choix, recommandation, pourquoi.
- Ajoute des tests de régression UX/range et du bug `risk_bb`.

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
