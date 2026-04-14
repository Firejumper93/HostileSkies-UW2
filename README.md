# Hostile Skies — Ultrawings 2 Combat Overhaul Mod

> **This mod is actively in development.** Core combat, the scrap economy, and the upgrade marketplace are fully functional. New features like island liberation, bomber escorts, and expanded progression are coming.

A MelonLoader mod for Ultrawings 2 (PC VR) that adds a full combat layer on top of free flight. Fight enemy AI, earn scrap from kills and engagements, spend it on upgrades in the marketplace, and push through escalating threat levels — all while flying any aircraft with tunable power settings.

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

## How to Activate Hostile Skies

Hostile Skies adds enemy AI combat to free flight. Here's exactly how to get it running:

### Step 1 — Cache Enemy Prefabs (Once Per Session)
Enemy prefabs only exist inside combat mission scenes. The mod grabs them automatically when you play one.

1. Start Ultrawings 2 normally and head to your office
2. Fly to any island and start **any combat mission** (Dogfight, Target Elimination, Air Defense, etc.)
3. The mod detects and caches all enemy prefabs in the background
4. You'll see `[COMBAT]` log messages confirming prefabs were found
5. **Quit the mission** or finish it — either way, return to free flight

> The mod saves the combat scene name to `Mods/UW2Trainer_Combat.txt`. On future sessions you can load prefabs directly from the Combat tab without replaying a mission.

### Step 2 — Activate Hostile Skies
1. In free flight, open the mod menu: **Spacebar** or **F1**
2. Go to the **Hostile Skies** tab
3. Verify prefab status shows **READY** for Messer and/or Wolf
4. Press **"Activate Hostile Skies"** on the floating panel
5. Choose your threat level (1–5) and press **"Start Engagement NOW"**

### Step 3 — Fight and Earn
- Enemy fighters spawn near you, turn toward you, and attack
- Weapons **auto-enable** when Hostile Skies is active
- **Right Trigger** = Primary weapon
- **A Button (hold)** = Secondary weapon (grenades, bombs — 1.2s cooldown)
- Your cockpit **EFI screen** shows kill count, wave number, scrap earned, and alerts
- Kill enemies to earn **scrap** — spend it in the **Upgrade Marketplace**

> **Important:** You must press "Activate Hostile Skies" BEFORE weapons and secondary fire will work. If your guns aren't firing, check that HS is toggled on.

---

## Scrap System

Scrap is the currency you earn through combat. Every kill, every wave cleared, and every engagement completed pays out scrap.

### How You Earn Scrap

| Action | Scrap Reward |
|--------|-------------|
| Kill a fighter (Messer/Wolf) | 100 scrap |
| Kill a turret / AA emplacement | 50 scrap |
| Kill a destroyer | 300 scrap |
| Kill an ace / special enemy | 500 scrap |
| Complete a wave | 200 x wave number (Wave 1 = 200, Wave 3 = 600, etc.) |
| Complete an engagement | 500 x threat level (Threat 2 = 1,000, Threat 5 = 2,500) |

### Kill Streaks
Consecutive kills without dying build your **streak multiplier**:
- Each kill in a streak adds **+0.1x** to the multiplier
- Caps at **2.0x** — meaning double scrap per kill at max streak
- Resets on death or engagement end

### Scrap Persistence
Your scrap balance, total kills, best streak, and all upgrade tiers are **saved to file** (`Mods/UW2Trainer_Combat.txt`) and persist between sessions.

---

## Upgrade Marketplace

Open the **Hostile Skies** tab in the mod menu to access the upgrade shop. Each upgrade has 4 tiers with increasing costs:

| Tier | Cost |
|------|------|
| Tier 1 | 500 scrap |
| Tier 2 | 1,500 scrap |
| Tier 3 | 4,000 scrap |
| Tier 4 | 10,000 scrap |

### Available Upgrades

| Upgrade | Effect Per Tier | Max (Tier 4) |
|---------|----------------|--------------|
| **Armor** | +25% HP | +100% HP |
| **Fire Rate** | -15% weapon cooldown | -60% cooldown |
| **Ammo Capacity** | +50% magazine size | +200% magazine |
| **Speed** | +20% engine power (also unlocks speed presets) | +80% power |
| **Handling** | +15% control response (pitch/roll/yaw) | +60% response |

The shop displays your current scrap balance, a progress bar for each upgrade `[>>>>----]`, and the cost of the next tier. Upgrades are applied immediately and persist across sessions.

### Speed Presets (Unlocked via Speed Upgrade)
As you upgrade Speed, new flight presets unlock:

| Preset | Power | Air Resistance | Notes |
|--------|-------|---------------|-------|
| Stock | 1.0x | 1.0x | Default handling |
| Sport | 2.0x | 0.7x | Unlocks at Speed Tier 1 |
| Combat | 3.0x | 0.5x | Unlocks at Speed Tier 2 |
| Ace | 5.0x | 0.3x | Unlocks at Speed Tier 3 |
| Afterburn | 5.0x | 0.2x | Unlocks at Speed Tier 4, includes boost |

---

## Combat System Details

### Threat Levels (1–5)
Higher threat = more enemies per wave, more waves per engagement, bigger payouts.

| Threat | Fighters Per Wave | Waves | Unlock Requirement |
|--------|------------------|-------|--------------------|
| 1 | 1–2 | 1–2 | Default |
| 2 | 2–3 | 2–3 | Default |
| 3 | 3–4 | 3–4 | Discover 3+ islands |
| 4 | 4–6 | 4–5 | Discover 5+ islands |
| 5 | 6–8 | 5–6 | Discover 5+ islands |

At Threat 4+, ambient encounters spawn between engagements while roaming.

### Combat State Machine
Hostile Skies cycles through these states automatically:

1. **ROAMING** — Weapons enabled, music playing, EFI hooked. Fly freely until you start an engagement.
2. **ENGAGEMENT** — Waves of enemies spawn based on threat level. Kill them all to clear the wave.
3. **WAVE COMPLETE** — 10-second pause, scrap awarded, then next wave or back to roaming.
4. **DEFEATED** — Triggered if you crash during combat. Streak resets.

### Battle Mode (Quick Spawns)
For instant action without the wave system, use Battle Mode presets:
- **Skirmish** — 2 enemies
- **Small Battle** — 4 enemies
- **Invasion** — 8 enemies
- **All Out War** — 15 enemies

### Enemy Types

| Enemy | Role | Armament | Scrap |
|-------|------|----------|-------|
| **Messer 01** | Light escort fighter | Machinegun | 100 |
| **Wolf 01** | Heavy fighter | Machinegun | 100 |
| **Junker** | Bomber | 2 turrets (top + rear) | 100 |
| **Snow Leopard A** | AA emplacement | 1 turret | 50 |
| **Destroyer 01/02** | Naval warship | 2–3 turrets | 300 |
| **Flak Cannon** | Ground defense | Proximity-fuse flak | 50 |
| **Transport Truck** | Ground target | Unarmed | 50 |

### EFI Cockpit Integration
When Hostile Skies is active, your in-cockpit EFI screen becomes a combat display:
- Live **scrap balance**, **kill count**, and **wave progress**
- **"ATTACKERS DETECTED"** alert on enemy spawns
- **Alert bell** sound effect on new waves
- Updates every second during combat

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
| **Y Button (hold 1.5s)** | Open mod menu while flying |
| **F2** | Toggle vehicle stats HUD |

### In-Flight Combat
| Input | Action |
|-------|--------|
| **Right Trigger** | Fire primary weapon |
| **A Button (hold)** | Fire secondary weapon (1.2s cooldown) |

### Wrist Panel
- **Hold Left Menu Button** to open
- 18 quick-access toggles, scrollable
- Works while flying without pausing

---

## Flight and Power Settings

### Flight Tab
| Feature | Description |
|---------|-------------|
| Engine Power | 2x or 5x thrust multiplier (per aircraft) |
| Air Resistance | Stock, Realistic Glide, Reduced, Low, Minimal drag presets |
| RPM Uncap | Remove the RPM limiter |
| ALL MAX | 5x power + realistic glide in one button |
| Reset to Stock | Revert all flight tweaks |
| Boost | Continuous forward thrust: Light (2K), Medium (10K), Heavy (50K), RIDICULOUS (200K) |
| Landing Mode | Reduces power and increases control for precision landings |

### Speed Presets (During Hostile Skies)
When HS is active, speed presets override manual flight settings — see the [Speed Presets table above](#speed-presets-unlocked-via-speed-upgrade).

### Vehicle Stats HUD (F2)
Press **F2** to toggle an overlay showing:
- Speed (m/s and knots), altitude
- Engine RPM and force
- Rigidbody drag and velocity
- Aircraft type and config

---

## Weapons

| Feature | Description |
|---------|-------------|
| Weapons in Free Flight | Force-enable aircraft weapons outside missions |
| Ammo Swap | Switch between bullet types (grenades, darts, Stallion rounds) |
| Grenade/Dart Equip | Equip handheld weapons |

---

## Cheats (Single-Player Only)

> **Fair Play:** All cheats are **automatically disabled in multiplayer sessions**. The mod detects active network connections and hard-disables these toggles during online play. Hostile Skies combat spawning is also disabled in multiplayer. These features are strictly for solo free flight and single-player missions.

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
| Dev Save (Slot 2) | Create a fully-unlocked save file |

---

## Music System

- Drop `.ogg` files into `UserData/HostileSkies/Music/`
- Toggle between original game music and Hostile Skies playlist from the Combat tab
- Next/previous track, volume control
- Game BGM automatically mutes when HS music is playing

---

## Additional Tabs

### Physics Tab
- Scan and modify aircraft physics configs in real time
- Direct access to flight model values

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

---

## File Structure

```
Mods/
  UW2TrainerMod.dll          - The compiled mod
  UW2Trainer_State.txt       - Persisted toggle states
  UW2Trainer_Combat.txt      - Scrap, kills, upgrades, combat scene name
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

## Known Limitations

- Enemy prefabs must be cached once per game session (play a combat mission or load from saved scene)
- The "Lightning" aircraft (vehicle ID 64) crashes on load — it's incomplete cut content
- Enemy AI operates within a local area; they won't follow across island boundaries
- Some enemies report `HasWeaponSystems = false` despite having working turrets

## What's Coming

- Island liberation campaign (9 islands, capture and defend)
- Bomber escort formations (Junker + Messer wingmen)
- Expanded weapon unlock progression (grenades, darts, rapid fire earned through kills)
- Ground vehicle targets and naval engagements
- Aircraft-specific roles (Interceptor, Multirole, Heavy Bomber, CAS)

## License

For personal use and educational purposes. Ultrawings 2 is developed by Bit Planet Games, LLC. This mod does not include any game assets or proprietary code.
