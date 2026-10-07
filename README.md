# Arcade

Borne d'arcade modulaire écrite en C++20 : un cœur unique charge dynamiquement ses
jeux **et** ses bibliothèques d'affichage à l'exécution, sous forme de bibliothèques
partagées. On peut passer d'un jeu à l'autre et d'un moteur graphique à l'autre sans
jamais recompiler ni relancer le programme — l'intérêt du projet est autant
l'architecture que les jeux eux-mêmes.

> **Epitech · `G-OOP-400` (« arcade »)** — projet d'équipe mené avec
> [Romane Cauvez](https://github.com/Romanecauvez) et
> [Thomas Peze](https://github.com/Thomas-Peze28).
>
> **Mon rôle :** développeur principal du projet.
>
> Ce dépôt est ma copie personnelle du rendu, publiée comme projet de portfolio.
> Le dépôt d'origine est privé.

---

## Architecture

Le cœur ne connaît que deux interfaces abstraites, déclarées dans `include/` :

| Interface | Rôle |
|---|---|
| `IGame` | Un jeu : état, entrées, rendu logique |
| `IDisplay` | Un moteur d'affichage : ouverture de fenêtre, dessin, entrées brutes |

`DLLoader` (`include/DLLoader.hpp`) ouvre les `.so` avec `dlopen` et résout les
symboles d'entrée ; `Arcade` orchestre la boucle principale et bascule de module à
chaud. Tout ce qui est chargé à l'exécution vit dans `lib/`.

## Jeux et affichages fournis

| Jeux | Bibliothèques graphiques |
|---|---|
| Snake | SFML |
| Démineur (Minesweeper) | SDL2 |
| | Ncurses |
| | Allegro5 |

## Compilation

```bash
make              # tout : cœur + jeux + bibliothèques graphiques
make core         # l'exécutable principal uniquement
make games        # les jeux       -> ./lib/
make graphicals   # les affichages -> ./lib/
make re           # fclean puis all
```

Prérequis : un compilateur C++20, `make`, et les bibliothèques graphiques
installées (SFML, SDL2, ncurses, Allegro5).

## Utilisation

```bash
./arcade [graphic_lib.so]
```

Le paramètre est la bibliothèque graphique de départ ; on peut ensuite en changer à
chaud. Un `compile_commands.json` est fourni pour l'intégration éditeur.

## Contrôles

| Touche | Action |
|---|---|
| Flèches ou `Z` `Q` `S` `D` | Se déplacer / naviguer dans les menus |
| `Entrée` | Action principale |
| `Espace` | Action secondaire |
| `F1` / `F2` | Bibliothèque graphique suivante / précédente |
| `F3` | Jeu suivant |
| `R` | Redémarrer le jeu en cours |
| `M` | Retour au menu principal |
| `Échap` | Quitter |

## Documentation

- [`doc/GAMES.md`](doc/GAMES.md) — implémenter un jeu (`IGame`)
- [`doc/GRAPHICS.md`](doc/GRAPHICS.md) — implémenter un module graphique (`IDisplay`)
- [`doc/CONTROLS.md`](doc/CONTROLS.md) — liste complète des contrôles

## Auteurs

- [Jean-Baptiste Lamy-Floret](https://github.com/007TheSpectre) — développeur principal
- [Romane Cauvez](https://github.com/Romanecauvez)
- [Thomas Peze](https://github.com/Thomas-Peze28)

L'interface partagée `IGame` / `IDisplay` a été définie en commun avec les autres
groupes de la promotion — merci à Fabien Skotarek, Enzo Sénéchal et Florent Windels.
