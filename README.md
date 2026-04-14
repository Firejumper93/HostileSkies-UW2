# Hostile Skies — Ultrawings 2 Combat Overhaul Mod

A MelonLoader mod for Ultrawings 2 (PC VR) that adds full air combat to free flight. Spawn enemy fighters that chase and attack you, manage weapons and ammo, play custom combat music, and tweak every aircraft in the game.

## Requirements

- **Ultrawings 2** (PC VR — Oculus/Steam)
- **MelonLoader** 0.5.x – 0.7.x ([Download](https://melonwiki.xyz/))
- **.NET 6 SDK** (only needed if building from source)

## Quick Install

1. Install MelonLoader into your Ultrawings 2 game directory
2. Launch the game **once** and close it (generates required assemblies)
3. Copy `UW2TrainerMod.dll` into the `Mods/` folder inside your game directory
4. Launch the game — press **Spacebar** or **F1** to open the mod menu

> **Tip:** An `install.bat` script is included that handles step 3 automatically.

### Building from Source
```bash
git clone https://github.com/Firejumper93/HostileSkies-UW2.git
cd HostileSkies-UW2
dotnet build UW2Mod.csproj
# DLL auto-copies to Mods/ folder via post-build
```

---

## How to Activate Hostile Skies (Combat Mode)

Hostile Skies is the combat system that spawns real enemy AI during free flight. Here's exactly how to get it running:

### Step 1 — Cache Enemy Prefabs (One-Time Setup)
Enemy prefabs only exist in combat mission scenes. The mod needs to grab them once per game session.

1. Start Ultrawings 2 normally and go to your office
2. Fly to any island and start **any combat mission** (Dogfight, Target Elimination, Air Defense, etc.)
3. The mod automatically detects and caches enemy prefabs in the background
4. You'll see `[COMBAT]` log messages confirming prefabs were found
5. **Quit the mission** (or finish it) and return to free flight

> After your first time, the mod saves the combat scene name to `Mods/UW2Trainer_Combat.txt`. On future sessions you can load prefabs from the Combat tab without replaying the mission.

### Step 2 — Activate Hostile Skies
1. Open the mod menu: **Spacebar** or **F1** (pauses the game)
2. Go to the **Combat** tab
3. Check the prefab status — it should say **READY** for Messer and/or Wolf
4. Press **"Activate Hostile Skies"** on the floating panel
5. Press **"Spawn 1 Enemy Fighter"** or choose a battle size:
   - Skirmish (2 enemies)
   - Small Battle (4 enemies)
   - Invasion (8 enemies)
   - All Out War (15 enemies)

### Step 3 — Fight
- Enemy fighters will spawn near you, turn toward you, and attack
- Your weapons auto-enable when Hostile Skies is active
- **Right Trigger** = Primary weapon (default fire)
- **A Button (hold)** = Secondary weapon (grenades, bombs — 1.2s cooldown)
- The in-cockpit EFI screen shows kill count, wave number, and alerts

> **Important:** You must activate Hostile Skies on the floating panel BEFORE weapons and secondary fire will work. If your guns aren't firing, check that HS is toggled on.

### Enemy Types
| Enemy | Type | Armament |
|-------|------|----------|
| **Messer 01** | Light escort fighter | Machinegun (SimpleTurret) |
| **Wolf 01** | Heavy fighter | Machinegun (SimpleTurret) |
| **Junker** | Bomber | 2 turrets (top + rear) |
| **Snow Leopard A** | AA emplacement | 1 turret |
| **Destroyer 01/02** | Naval warship | 2–3 turrets |
| **Flak Cannon** | Ground defense | Proximity-fuse flak |
| **Transport Truck** | Ground target | Unarmed (scrap target) |

---

## Controls

### Menu
| Input | Action |
|-------|--------|
| **Spacebar / F1** | Toggle mod menu (pauses game) |
| **Left Thumbstick** | Navigate up/down, adjust sliders left/right |
| **Right Thumbstick** | Switch tabs left/right |
| **A Button (Right)** | Activate / confirm |
| **B Button (Right)** | Back / close menu |
| **Y Button (hold 1.5s)** | Open mod menu (in-flight) |
| **F2** | Toggle vehicle stats HUD |

### In-Flight Combat
| Input | Action |
|-------|--------|
| **Right Trigger** | Fire primary weapon |
| **A Button (hold)** | Fire secondary weapon |

### Wrist Panel
- **Hold Left Menu Button** to open
- 18 quick-access toggles, scrollable
- Works while flying without pausing

---

## Features

### Combat Tab
| Feature | Description |
|---------|-------------|
| Hostile Skies Toggle | Activate/deactivate combat mode |
| Spawn Fighters | Spawn 1, or battle presets (2/4/8/15 enemies) |
| Load Enemy Prefabs | Load from saved combat scene without replaying a mission |
| Weapons in Free Flight | Force-enable aircraft weapons outside missions |
| Ammo Swap | Switch between bullet types |
| Grenade/Dart Equip | Equip handheld weapons |
| Laser Designator | Activate laser targeting |
| Scan / Deep Scan | Search for all combat-capable assets in memory |

### EFI Cockpit Integration
When Hostile Skies is active, the in-cockpit EFI screen shows:
- **Kill count** and **wave number** (updates live)
- **"ATTACKERS DETECTED"** alert when enemies spawn
- **Enemy alert bell** sound on new spawns
- Scrap/score display on the earnings line

### Music System
- Drop `.ogg` files into `UserData/HostileSkies/Music/`
- Toggle between original game music and Hostile Skies playlist
- Next/previous track, volume control from Combat tab
- Game BGM automatically mutes when HS music is playing

### Sandbox Tab (Single-Player Only)

> **Fair Play:** All sandbox features are **automatically disabled in multiplayer sessions**. The mod detects active Photon network connections and hard-disables sandbox toggles to prevent any unfair advantage. These features are strictly for solo free flight and single-player missions.

| Feature | Description |
|---------|-------------|
| Unlimited Fuel | Never run out of fuel |
| Unlimited Ammo | Infinite ammunition |
| God Mode | Invulnerable + no crash damage |
| Money Editor | Adjust in-game currency |
| Unlock All Vehicles | Phoenix, Stallion, Comet, NewHawk, Dragonfly, Kodiak |
| Vehicle Swap | Fly any aircraft in any mission |
| Weather Control | Day, Sunset, Night, Overcast, Auto |
| Unlock All Missions | Access all mission types |
| Disable Crashes | Turn off crash detection |
| Manual Save | Force save without entering a mission |

### Flight Tab
| Feature | Description |
|---------|-------------|
| Force Multiplier | 2x or 5x engine thrust (per aircraft) |
| Drag Reduction | Lower drag for higher top speed |
| RPM Uncap | Remove RPM limiter |
| Boost | Temporary speed burst |
| Per-aircraft settings | Each aircraft type has independent controls |

### Physics Tab
- Scan and modify aircraft physics configs in real time
- Direct access to `AircraftControllerConfigDO` values

### Aircraft Tab
- Scan aircraft models and mesh renderers
- Model swap experiments

### Explore Tab
| Feature | Description |
|---------|-------------|
| Hidden Content Scan | Search for ships, carriers, rigs, military objects |
| Vehicle/Traffic Scan | Find all vehicle components in scene |
| Carrier Diagnostic | Aircraft Carrier location system state |
| Quality Override | Force HIGH material quality |

### Info Tab
- Player data dump (money, unlocks, mission progress)
- Current aircraft stats and game state

### Diagnostics Tab
- Real-time engine/physics readouts
- Component inspection and performance monitoring

## Vehicle Stats HUD (F2)

Press **F2** to toggle an overlay showing:
- Speed (m/s and knots), altitude
- Engine RPM and force
- Rigidbody drag and velocity
- Aircraft type and config

---

## File Structure

```
Mods/
  UW2TrainerMod.dll          - The compiled mod
  UW2Trainer_State.txt       - Persisted toggle states
  UW2Trainer_Combat.txt      - Combat progression + saved scene name
UserData/
  HostileSkies/
    Music/                   - Drop .ogg files here for combat music
```

## Technical Notes

- MelonLoader mod for IL2CPP Unity games
- Uses `Il2CppInterop` to access game internals at runtime
- Enemy AI uses the game's native `AirDefenseEnemyAIController` and `AiAircraftController`
- Prefabs cloned with `DontDestroyOnLoad` to survive scene transitions
- Scene hook (`OnSceneWasLoaded`) auto-scans combat missions for enemy assets
- EFI integration hooks into `AssaultMissionController` signals for cockpit display
- All modifications are runtime-only — no game files are changed

## Multiplayer Safety

This mod is designed for **single-player use**. All sandbox features (unlimited fuel/ammo, god mode, money, unlocks, etc.) are **automatically disabled when a multiplayer session is detected**. The mod checks for active Photon network connections and will not allow sandbox toggles to activate during online play. Hostile Skies combat spawning is also disabled in multiplayer to prevent disruption to other players.

## Known Limitations

- Enemy prefabs must be cached once per game session (play a combat mission or load from saved scene)
- The "Lightning" aircraft (vehicle ID 64) crashes on load — it's incomplete cut content
- Enemy AI operates within a local area; they won't follow across island boundaries
- Some enemies report `HasWeaponSystems = false` despite having working turrets

## Hidden Content Discovered

- **Aircraft Carrier** — UI signals exist for a planned carrier location that was never finished
- **Cut Aircraft** — "Lightning" vehicle type in the enum but incomplete

## License

For personal use and educational purposes. Ultrawings 2 is developed by Bit Planet Games, LLC. This mod does not include any game assets or proprietary code.
