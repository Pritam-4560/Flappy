# Flapocalypse (working title)


Side-scrolling, one-tap Flappy Bird with a long map (3,000 m, five zones, three guardian bosses).
Each death banks scrap; permanent upgrades (Hull, Wings, Salvage, Shortcut Cannons) help you get further
until you can finish the whole map in a single run. Tap / click / space to flap. Open `index.html`.

## Art
Rivet (the bird) is rendered with [SpriteKiln](https://github.com/LucasJRamos/spritekiln) (free, MIT) from `art/art/specs/characters/rivet/rivet.yaml`;
the atlas is `assets/rivet_kiln.png` and is also embedded in `index.html`. From update 1.5 the whole game is drawn
then snapped to a 100x160 pixel grid with a limited palette, with a bitmap font for text.
