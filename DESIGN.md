# FROZEN FACTORY - Complete Design Reference

## Quick Reference
- **Map:** 512x512, wraps around, fog of war
- **Day/Night:** Planet-dependent (10/15 min on Terra Prime)
- **Inventory:** 16 slots
- **Currency:** Credits
- **Save:** Auto every 5 seconds to localStorage
- **Cheat code:** Type "levitysm" anywhere

---

## PLAYER ROBOT

### Stats
- 16 inventory slots
- Built-in heater (low power consumption)
- Built-in battery (lasts 2 full day/night cycles, upgradable)
- CAN FREEZE if battery dies

### Freeze/Death
- When battery hits 0: Robot freezes in place
- **Rescue Mode:** Wait for sun to thaw OR Sun Tracker robot finds you
- Does NOT lose inventory on freeze
- Frequent freezing = robot needs repairs

### Movement
- WASD isometric movement
- Collision with machines/terrain
- Can push small items

---

## TEMPERATURE SYSTEM

### Machine States
| State | Color | Efficiency | Notes |
|-------|-------|------------|-------|
| Optimal | Green | 100% | Normal operation |
| Cold | Blue | 50% | Warning, still works |
| Frozen | White | 0% | Stopped, needs thaw |
| Overheated | Orange | 100% | Fire risk! |
| On Fire | Red | 0% | Spreading damage |

### Heat Formula
```
Temperature = PlanetBase + SunHeat + HeaterHeat - ColdDecay - CoolingEffect

PlanetBase: Varies by planet (-10 to -50)
SunHeat: +30 during day, 0 at night
HeaterHeat: +20 base, decays with distance (inverse square)
ColdDecay: -5/sec base (faster on harder planets)
CoolingEffect: From pipes/heatsinks (prevents overheating)
```

### Heat Distance Decay
- Adjacent tile: 100% heat
- 2 tiles away: 50% heat
- 3 tiles away: 25% heat
- 4+ tiles: negligible

---

## COOLING SYSTEMS

### Passive Cooling
- **Heat Sink:** Absorbs excess heat, prevents fire
- **Copper Wiring:** Conducts heat away from machines

### Active Cooling
- **Fan:** Uses power, actively cools area
- **Snow Pipe System:** Early game - mine snow, pipe past machines
- **Water Coolant Loop:** Late game - closed circuit, more efficient

### Snow vs Water
| System | Availability | Efficiency | Complexity |
|--------|--------------|------------|------------|
| Snow Pipes | Early | Low | Simple - just pump snow |
| Water Loop | Mid-Late | High | Needs: Water Miner, pipes, radiator |

---

## FIRE SYSTEM

### Ignition
- Heaters at max power 60+ seconds = fire risk
- Risk increases with heat level
- No cooling = guaranteed fire eventually

### Spread
- Fire spreads to adjacent tiles every 5 seconds
- Diagonal spread at 50% chance
- Burning machines take 10 damage/second
- Machines explode at 0 HP (destroys machine, damages adjacent)

### Suppression
- **Fire Extinguisher Station:** Auto-suppress, 5 tile radius, upgradable
- **Manual Extinguisher (E key):** Player aims and sprays, unlimited use
- Water pipes passing through fire = instant extinguish that tile

---

## POWER SYSTEM

### Generation
| Source | Output | Condition | Notes |
|--------|--------|-----------|-------|
| Solar Panel | 10 power | Day only | Free, reliable |
| Generator | 15 power | Always | Burns 1 coal/30sec |
| Battery | Storage | N/A | Holds 100 power units |

### Consumption (per second)
| Machine | Power Draw |
|---------|------------|
| Miner | 2 |
| Water Miner | 3 |
| Furnace | 4 |
| Assembler | 5 |
| Heater | 3 |
| Heat Lamp | 1 |
| Fan | 2 |
| Conveyor | 0.5 |
| Lights | 0.5 |
| Fire Extinguisher | 1 (idle), 5 (active) |

### Power Flow
- Power cables connect machines
- No cable = no power
- Batteries charge when excess, discharge when deficit

---

## MACHINES

### Mining
| Machine | Function | Notes |
|---------|----------|-------|
| Miner | Extracts ore from nodes | Nodes deplete! |
| Water Miner | Drills ice for water | Requires ice terrain |

### Processing
| Machine | Input | Output | Time |
|---------|-------|--------|------|
| Furnace | 2 Iron Ore | 1 Iron Ingot | 5s |
| Furnace | 2 Copper Ore | 1 Copper Ingot | 5s |
| Furnace | 1 Iron + 1 Coal | 1 Steel | 8s |
| Assembler | (various recipes) | (various) | varies |
| Fuel Refinery | Special recipe | Super Fuel | 30s |
| 024 Refiner | 024 Ore | Any resource | 10s |

### Heat Management
| Machine | Function | Risk |
|---------|----------|------|
| Heater | +20 heat to nearby tiles | FIRE RISK |
| Heat Lamp | +8 heat, safer | Low risk |
| Heat Sink | Absorbs excess heat | None |
| Fan | Active cooling | None |

### Automation
| Machine | Function |
|---------|----------|
| Conveyor Belt | Moves items between machines |
| Pipe | Moves liquids/snow (slower) |
| Storage Crate | Holds 32 item stacks |

### Special
| Machine | Function |
|---------|----------|
| Landing Pad | Planet travel (needs Super Fuel) |
| Lights | Illuminates area at night |
| Fire Extinguisher Station | Auto-suppresses fires |
| Sun Tracker Robot | Autonomous solar collector |
| Repair Robot | Fixes freeze-damaged machines |

---

## SUN TRACKER ROBOT

### Behavior
1. Leaves battery bank with empty batteries
2. Travels toward sun position
3. Charges batteries using built-in solar
4. Returns to bank, deposits charged batteries
5. Repeat

### Stats
- Needs fuel to operate (small amount)
- Net positive energy gain
- Can build multiple for more throughput
- Each robot: 1 charged battery per cycle

### Building
- Requires: 5 Steel, 3 Circuits, 2 Solar Panels
- Also need Battery Bank structure

---

## REPAIR ROBOT

### Behavior
- Patrols your factory
- Detects damaged machines
- Automatically repairs them
- Returns to charging station when low power

### Stats
- Repair speed: 10 HP/second
- Power consumption: 2/second while working
- Can build multiple for larger factories

---

## RESOURCES

### Raw (Mined)
| Resource | Found On | Rarity |
|----------|----------|--------|
| Iron Ore | All planets | Common |
| Copper Ore | All planets | Common |
| Coal | All planets | Common |
| Crystal | Frost Moon+ | Uncommon |
| Dark Matter | Shadow Belt+ | Rare |
| Quantum Ore | Ice Giant+ | Very Rare |
| 024 | Space Rock-024 only | Infinite nodes |

### Processed
| Resource | Recipe |
|----------|--------|
| Iron Ingot | 2 Iron Ore @ Furnace |
| Copper Ingot | 2 Copper Ore @ Furnace |
| Steel | 1 Iron Ingot + 1 Coal @ Furnace |
| Circuit | 2 Copper Ingot + 1 Crystal @ Assembler |
| Engine Part | 3 Steel + 1 Circuit @ Assembler |
| Super Fuel | 2 Dark Matter + 1 Quantum Ore + 5 Coal @ Fuel Refinery |

### Special
| Resource | Use |
|----------|-----|
| Water | Coolant loops, some recipes |
| Snow | Crude cooling, can be piped |
| Super Fuel | Planet travel |
| 024 Refined | Can become ANY other resource |

---

## CRAFTING RECIPES (ASSEMBLER)

### Basic (Early Game)
| Output | Inputs | Time |
|--------|--------|------|
| Cable (x5) | 1 Copper Ingot | 3s |
| Pipe (x3) | 2 Iron Ingot | 4s |
| Conveyor (x2) | 1 Iron Ingot, 1 Copper Ingot | 5s |

### Intermediate (Mid Game)
| Output | Inputs | Time |
|--------|--------|------|
| Circuit | 2 Copper Ingot, 1 Crystal | 8s |
| Heat Sink | 3 Copper Ingot, 1 Iron Ingot | 6s |
| Solar Panel | 2 Crystal, 2 Copper Ingot, 1 Steel | 12s |
| Battery | 2 Copper Ingot, 1 Crystal, 1 Iron Ingot | 10s |

### Advanced (Late Game)
| Output | Inputs | Time |
|--------|--------|------|
| Engine Part | 3 Steel, 1 Circuit | 15s |
| Sun Tracker Robot | 5 Steel, 3 Circuit, 2 Solar Panel | 45s |
| Repair Robot | 4 Steel, 2 Circuit, 1 Engine Part | 40s |
| Super Fuel | 2 Dark Matter, 1 Quantum Ore, 5 Coal | 30s |

### Endgame (Space Rock-024)
| Output | Inputs | Time |
|--------|--------|------|
| 024 Refiner | 10 Steel, 5 Circuit, 3 Engine Part, 1 Dark Matter | 120s |
| Refined 024 -> Any | 1 024 Ore | 10s |

---

## PLANETS

### Terra Prime (Starting)
- Day: 10 min | Night: 15 min
- Base Temp: -10
- Resources: Iron, Copper, Coal
- Special: Tutorial area near spawn

### Frost Moon
- Day: 8 min | Night: 17 min
- Base Temp: -20
- Resources: Iron, Copper, Coal, **Crystal**
- Special: More ice terrain, water mining easier

### Shadow Belt
- Day: 5 min | Night: 20 min
- Base Temp: -30
- Resources: All previous + **Dark Matter**
- Special: Dark Matter nodes glow purple

### Ice Giant
- Day: 3 min | Night: 22 min
- Base Temp: -40
- Resources: All previous + **Quantum Ore**
- Special: Quantum nodes are unstable, mining has small explosion risk

### Space Rock-024
- Day: NONE | Night: ALWAYS
- Base Temp: -50
- Thaw Rate: 50% slower
- Freeze Rate: 50% faster
- Resources: **024 only** (infinite nodes)
- WARNING: Bring excess power and fuel!
- Special: 024 Refiner unlocked here

---

## ECONOMY

### NPCs
| NPC | Buys | Sells | Location |
|-----|------|-------|----------|
| Scrap Dealer | Raw ore | Basic machines | Near spawn |
| Parts Merchant | Processed items | Advanced machines | Mid-map |
| Collector | Rare items | Special items | Far from spawn |

### Prices (Credits)
**Selling:**
| Item | Price |
|------|-------|
| Iron Ore | 2 |
| Copper Ore | 3 |
| Coal | 2 |
| Iron Ingot | 8 |
| Copper Ingot | 10 |
| Steel | 20 |
| Crystal | 25 |
| Circuit | 50 |
| Dark Matter | 100 |
| Quantum Ore | 200 |

**Buying (from NPCs):**
| Item | Price |
|------|-------|
| Miner | 50 |
| Furnace | 80 |
| Heater | 40 |
| Solar Panel | 100 |
| Battery | 60 |
| Assembler | 150 |

### Bulk Bonus
- 10+ items: 10% bonus
- 25+ items: 20% bonus
- 50+ items: 30% bonus

---

## CONTROLS

| Key | Action |
|-----|--------|
| WASD | Move robot |
| Mouse Wheel | Zoom in/out |
| Middle Mouse Drag | Pan camera |
| Left Click | Interact / Place building |
| Right Click | Open machine menu / Cancel |
| R | Rotate building |
| E | Use extinguisher / Pick up item |
| Q | Drop held item |
| Space | Pause game |
| Tab | Build menu |
| I | Inventory |
| M | Full map view |
| F | Toggle camera follow |

---

## CHEAT MENU

**Activation:** Type "levitysm" anywhere in game

### Options
| Cheat | Effect |
|-------|--------|
| Add Battery | Instantly refill robot battery |
| Add Warmth | Set robot temp to optimal |
| Add Items | Opens item spawner menu |
| Free Crafting | All recipes cost nothing |
| Lantern | Reveals entire map (removes fog) |
| No Death | Robot cannot freeze/die |
| Rocket Launcher | Equip multi-mode launcher |

### Rocket Launcher Modes
1. **Destroy:** Click machine to instantly destroy it
2. **Clear:** Click terrain to remove ice/obstacles in radius
3. **Launch:** Click ground to fling robot to that location

---

## TUTORIAL LOADOUT (Starting Setup)

Player spawns near pre-placed:
- 1 Miner (on iron node)
- 1 Solar Panel (connected)
- 1 Small Heater (keeps miner warm during day)
- 1 Storage Crate
- 1 Battery (partially charged)
- 5 Iron Ore in crate
- 3 Coal in crate

This gives continuous warmth during day and crude resource production to bootstrap.

---

## UI LAYOUT

```
+----------------------------------------------------------+
| [Resources: Fe Cu Coal etc]    [Day/Night] [Temperature] |
| [Credits: XXX]                 [Sun Position]            |
+----------------------------------------------------------+
|                                                          |
|                                                          |
|                    GAME WORLD                            |
|                    (Isometric)                           |
|                                                          |
|  +--------+                                              |
|  | Mini   |                                              |
|  | Map    |                                              |
|  +--------+                                              |
+----------------------------------------------------------+
| [Build Menu]  [Selected Machine Info]  [Robot Status]    |
+----------------------------------------------------------+
```

### Color Themes (Player Choice at Startup)
1. **Cold Blue/White** - Icy, matches world
2. **Warm Orange/Amber** - Cozy industrial
3. **Green Terminal** - Retro sci-fi
4. **High Contrast** - Accessibility option

---

## MACHINE DURABILITY

### Freeze Damage
- Each time a machine fully freezes: -5 max HP
- Damaged machines show cracks/sparks
- At 50% HP: efficiency reduced to 75%
- At 25% HP: efficiency reduced to 50%
- At 0 HP: machine breaks, drops some materials

### Repair
- **Manual:** Walk to machine, hold E, costs repair materials
- **Repair Robot:** Automatic, patrols and fixes

### Repair Costs
| Machine Tier | Materials |
|--------------|-----------|
| Basic (Miner, etc) | 1 Iron Ingot |
| Medium (Furnace, etc) | 1 Steel |
| Advanced (Assembler, etc) | 1 Steel + 1 Circuit |

---

## SAVE DATA STRUCTURE

```javascript
{
  version: 1,
  planet: "terra_prime",
  dayTime: 0.0-1.0,
  robot: { x, y, inventory[], battery, temp, hp },
  machines: [{ type, x, y, hp, temp, inventory, settings }],
  resources: [{ type, x, y, amount }],
  explored: [[bool]], // fog of war
  npcs: [{ type, x, y, inventory, prices }],
  stats: { credits, playtime, machinesBuilt, ... },
  cheats: { enabled: false, active: [] },
  settings: { colorTheme, volume, ... }
}
```

Auto-saves every 5 seconds to localStorage key: "frozen_factory_save"
