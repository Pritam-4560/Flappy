# Flapocalypse (working title)

The Big Climb: one huge vertical map (5,000 m). Flap up through ledges, stomp drones, grab launchers, beat 3 guardians. Permanent upgrades let you climb higher each run until you can reach the summit in one run.

Play: open `index.html` (no build step). Space / click / tap to flap. Progress saves in `localStorage`.

## Design as implemented in the prototype
- **Scrap**: collected in gaps (cyan = x5). Banked on death, spent on permanent upgrades in the menu.
- **Temp upgrades**: pick 1 of 3 every 5 pipes (and after each boss). 9 types, some stackable.
- **Permanent upgrades**: Scrap Armor, Magpie Beak, Light Wings, Wide Berth, Chaos Magnet, Fourth Option.
- **Chaos Meter**: fills from near-misses (+14) and scrap (+3). At 100% → 8s Chaos: world +20% speed, gaps wobble, **2x scrap**.
- **Boss** (every 15 pipes): The Great Pigeon fires telegraphed horizontal beams for 12s; survive for scrap + a free pick. More beams per later boss.
- **Difficulty**: speed rises with pipes passed, gap shrinks to a floor.

## Still to do
- Final name, art/audio, mobile wrapper, balance pass from playtests, more boss types, deeper upgrade tree.
