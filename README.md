# game_1

## Confirmed architecture and stack

- **Engine:** Unity (C#)
- **Game Type:** 2D top-down zombie survival with base management and NPC psychology
- **Code Structure:** Hybrid MVC + ECS-style simulation split
  - **Simulation (Model):** AI math, action resolution, sanity/relationship systems, economy
  - **Presentation (View/Controller):** Rendering, animation, input adapters, HUD
  - Simulation must run independently from rendering update loops to keep mobile thermals stable.
- **Persistence:** Versioned JSON save data (binary optional later), storing:
  - NPC psychological state and traits
  - NPC-to-NPC relationship matrix
  - Inventory/resources and base zones
  - Automation assignments and world state

## Global measurement standard (mandatory)

All internal logic and UI must use:

- **kg** for weights, carrying limits, and inventory mass
- **km** for map distances, movement path lengths, and assignment node ranges

No alternate units should be surfaced in gameplay logic or UI.

## Core gameplay systems to implement

1. **Player Avatar Control**
   - Direct movement/combat/build interaction as settlement leader.
2. **Base Building**
   - Place and manage functional zones (farm, barricade, armory, etc.).
3. **Automation & Assignment**
   - Assign NPCs to task nodes (local and distant km-based nodes) with looped pathfinding tasks.
4. **Resource Economy**
   - Manage food/water/materials under total group carrying capacity (**kg**) and consumption.
5. **Unreliability Engine (Action Modifiers)**
   - Dynamic accuracy from stress
   - Weapon jam probability from durability
   - Panic outcomes (fumble, freeze, reload disruption)
   - Unified action resolver for both player and automated NPC actions
6. **NPC Deep Psychology**
   - Hidden/visible traits (e.g., Coward, Introvert, Betrayer, Leader)
   - Dynamic sanity/mental-state meter
   - Social relationship matrix
   - Daily conflict event generator (theft/arguments/murder risk triggers)
7. **UI/UX**
   - Shared interaction logic for PC mouse and mobile tap
   - Clear emotional/resource state visibility
   - Responsive layouts for phone portrait and PC landscape

## Visual and animation direction

- **Theme:** Gritty post-apocalyptic zombie survival
- **Art style:** Clean, low-clutter 2D visuals
- **Animation:** 2D skeletal rig workflows (engine-native rigging/Spine-compatible pipeline)
  - Supports dynamic emotional overlays (e.g., slumped shoulders, panic hand shake)

## Recommended implementation phases

1. Establish simulation domain models and strict kg/km utility types.
2. Implement save/load schema with migration versioning.
3. Build action resolver + unreliability mechanics.
4. Build NPC psychology + social/conflict systems.
5. Add base building + automation loops.
6. Integrate unified input and responsive UI layers.
7. Polish animation blending and feedback icons.