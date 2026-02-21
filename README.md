# Penguin Change

**[Play it here](https://frozen-future.pages.dev/)**

A browser-based pixel art game built for the **Games for Change Student Challenge (2024)** under the theme *Stronger and Greener Communities*.

Players witness the effects of carbon emissions on a penguin colony living on a melting iceberg. Coal power plants generate emissions that cause ice tiles to break away at the edges, shrinking the habitat and stranding penguins in the water. The goal is to understand the relationship between fossil fuel infrastructure and habitat loss.

## Gameplay

- **15 penguins** wander freely across a tile-based iceberg surrounded by ocean.
- A **coal power plant** sits on the ice, driving an emissions counter that determines how fast the iceberg melts.
- Players **upgrade power plants** through a progression: **Coal → Solar → Wind → Nuclear**. Each tier produces less pollution than the last -- solar and wind still have a small environmental footprint due to manufacturing and land use, while nuclear is the cleanest option.
- Ice tiles break off randomly from the edges over time -- higher emissions mean faster melting.
- Penguins that end up in the water become stranded and stop moving.
- Players can **click and drag penguins** to relocate them on the remaining ice.
- A **hover cursor** highlights tile placement areas, tinting red when the position is invalid.

## Tech Stack

- **TypeScript** with **Vite** for bundling and dev server
- **PixiJS v8** for WebGL/Canvas 2D rendering
- Custom pixel art spritesheets (16x16 penguin tiles, 16x16 iceberg tiles, 32x32 power plant tiles)

## Project Structure

```
src/
  main.ts                  # App entry -- sets up tilemap layers, spawns penguins, runs melt loop
  stage.ts                 # Game loop manager, adds/removes bodies from the PixiJS ticker
  body.ts                  # Abstract base class for game entities (position, sprite, movement)
  movement.ts              # Abstract movement strategy interface
  direction.ts             # Direction enum and helpers (point conversion, random direction)
  pointMath.ts             # Vector math utilities (add, subtract, multiply, distance, bounds)

  bodies/
    penguin.ts             # Penguin entity -- animated sprite, drag-and-drop, water detection

  movements/
    penguinMovement.ts     # Random walk that avoids iceberg edges and blocking tiles
    randomMovement.ts      # Simple random movement (8-directional)
    emptyMovement.ts       # No-op movement (used when penguin is held or in water)

  tilemap/
    tilemap.ts             # Abstract tilemap with tile CRUD, collision queries, hover support
    baseTilemap.ts         # Concrete base tilemap (water layer)
    overlayTilemap.ts      # Layered tilemap that delegates existence checks to a parent layer
    tilemap2x2.ts          # Tilemap variant for 2x2 tile structures (power plants)
    overlayTilemap2x2.ts   # Overlay version of 2x2 tilemap
    tile.ts                # Individual tile -- sprite, position, click/hover events
    tileFlag.ts            # Tile flag enum (SOLID, BLOCKING)
    hoverSprite.ts         # Cursor overlay that follows the mouse over valid tiles

  penguinSpritesheet.ts    # Penguin spritesheet definition and loader
  icebergSpritesheet.ts    # Iceberg/water tile spritesheet definition and loader
  powerPlantSpritesheet.ts # Power plant spritesheet definition and loader (coal, solar, wind, nuclear)

public/
  penguin.png              # Penguin spritesheet
  icebergtiles.png         # Iceberg and water tile spritesheet
  powerPlants.png          # Power plant spritesheet
  hover.png                # Tile hover cursor sprite
  style.css                # Minimal CSS (centered canvas, pixelated rendering)
```

## Getting Started

```bash
# Install dependencies
npm install

# Start the dev server
npm run dev

# Build for production
tsc && npm run build

# Preview production build
npm run preview
```

## How It Connects to the Theme

The game illustrates how fossil fuel emissions directly threaten wildlife habitats. As the power plants emit pollution, the iceberg -- home to the penguin colony -- shrinks tile by tile. Players experience the urgency of climate action by watching penguins lose their ground and fall into the ocean, reinforcing the need for stronger and greener energy choices to protect vulnerable communities -- both human and animal. The game also underlines the path to completely green energy, showing how progress towards a green world can be made over time through small steps.
