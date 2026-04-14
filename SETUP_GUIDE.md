# Hostile Skies — Setup Guide

Complete setup and gameplay guide for the Hostile Skies combat mod for Ultrawings 2.

---

## Prerequisites

- **Ultrawings 2** installed (PC VR — Oculus or Steam)
- A VR headset (Quest via Link/Air Link, Rift, Index, etc.)

---

## Part 1: Install MelonLoader

MelonLoader is the mod framework that lets Hostile Skies run inside UW2.

1. Download **MelonLoader Installer** from https://github.com/LavaGang/MelonLoader/releases
   - Get `MelonLoader.Installer.exe` (v0.5.x – v0.7.x all work)
2. Run the installer
3. Click **SELECT** and browse to your Ultrawings 2 executable:
   - **Oculus:** `C:\Program Files\Oculus\Software\Software\bit-planet-games-llc-ultrawings-2\Ultrawings 2.exe`
   - **Steam:** `C:\Program Files (x86)\Steam\steamapps\common\Ultrawings 2\Ultrawings 2.exe`
4. Make sure **IL2CPP** is selected as the game type (should auto-detect)
5. Click **INSTALL**
6. **Launch Ultrawings 2 once and close it** — this generates the managed assemblies MelonLoader needs

After this step you should see a `MelonLoader/` folder and a `Mods/` folder inside your game directory.

---

## Part 2: Install the Mod

### Option A: Pre-built DLL (Easiest)
1. Download `UW2TrainerMod.dll` from the [Releases](https://github.com/Firejumper93/HostileSkies-UW2/releases) page
2. Copy `UW2TrainerMod.dll` into the `Mods/` folder inside your game directory
3. Done — launch the game

### Option B: Use the Install Script
1. Download or clone the repo
2. Run `install.bat` — it copies the DLL to the correct location automatically

### Option C: Build from Source
```bash
git clone https://github.com/Firejumper93/HostileSkies-UW2.git
cd HostileSkies-UW2
dotnet build UW2Mod.csproj
```
The post-build script auto-copies the DLL to your `Mods/` folder. Requires .NET 6 SDK.

---

## Part 3: First Launch

1. Launch Ultrawings 2 with your VR headset connected
2. You'll see MelonLoader console messages during startup — this is normal
3. Once you're in the game office, press **Spacebar** or **F1** to open the mod menu
4. You should see the Hostile Skies menu with 8 tabs

If the menu doesn't appear, check `MelonLoader/Latest.log` for errors.

---

## Part 4: Activating Hostile Skies (Combat Mode)

Enemy fighters don't exist in free flight by default — the mod needs to grab them from a combat mission first.

### First Time Setup (Once Per Session)

1. From your office, fly to any island
2. Start **any combat mission** — Dogfight, Target Elimination, Air Defense, etc.
3. Wait a few seconds for the mission to load
4. The mod automatically detects and caches all enemy prefabs in the background
5. You can quit the mission immediately or finish it — either way the prefabs are saved
6. Return to free flight

> The mod saves the combat scene name to `Mods/UW2Trainer_Combat.txt`. On future sessions, you can load prefabs directly from the Hostile Skies tab without replaying a mission.

### Activating Combat

1. In free flight, press **Spacebar/F1** to open the mod menu
2. Go to the **Hostile Skies** tab
3. Verify prefab status shows **READY** for Messer and/or Wolf
4. Press **"Activate Hostile Skies"** on the floating panel
5. Choose your **Threat Level** (1–5)
6. Press **"Start Engagement NOW"** or use a Battle Mode preset:
   - **Skirmish** — 2 enemies
   - **Small Battle** — 4 enemies
   - **Invasion** — 8 enemies
   - **All Out War** — 15 enemies
7. Close the menu and fight!

### Combat Controls

| Input | Action |
|-------|--------|
| **Right Trigger** | Fire primary weapon |
| **A Button (hold)** | Fire secondary weapon (1.2s cooldown) |
| **Spacebar / F1** | Open menu to spawn more enemies or adjust settings |

### What You'll See

- Enemy fighters spawn near you and immediately attack
- Your cockpit **EFI screen** shows kill count, wave number, scrap earned, and combat alerts
- An **alert bell** sounds when new enemies spawn
- Weapons **auto-enable** when Hostile Skies is active

> **If your weapons aren't firing:** Make sure you pressed "Activate Hostile Skies" on the floating panel first. Weapons require HS to be toggled on.

---

## Part 5: Earning Scrap and Using the Marketplace

### How Scrap Works
Scrap is the combat currency. You earn it by fighting and spend it on permanent upgrades.

| Action | Scrap Earned |
|--------|-------------|
| Kill a fighter | 100 |
| Kill a turret / AA | 50 |
| Kill a destroyer | 300 |
| Kill an ace | 500 |
| Clear a wave | 200 x wave number |
| Complete an engagement | 500 x threat level |

**Kill streaks** increase your multiplier by +0.1x per consecutive kill, up to 2.0x. Dying or ending an engagement resets the streak.

### Upgrade Marketplace
In the Hostile Skies tab, scroll down to the **UPGRADES** section. Your current scrap balance is shown at the top.

Each upgrade has 4 tiers costing **500 / 1,500 / 4,000 / 10,000** scrap:

| Upgrade | What It Does | Max Tier Effect |
|---------|-------------|-----------------|
| **Armor** | +25% HP per tier | +100% HP |
| **Fire Rate** | -15% weapon cooldown per tier | -60% cooldown |
| **Ammo Capacity** | +50% magazine size per tier | +200% ammo |
| **Speed** | +20% engine power per tier + unlocks speed presets | +80% power |
| **Handling** | +15% pitch/roll/yaw response per tier | +60% response |

Upgrades apply immediately and persist between sessions. The shop shows a progress bar for each upgrade and the cost of the next tier.

### Speed Presets
The Speed upgrade unlocks flight presets that change how your aircraft handles:

| Preset | Power | Air Resistance | Unlock |
|--------|-------|---------------|--------|
| Stock | 1.0x | 1.0x | Default |
| Sport | 2.0x | 0.7x | Speed Tier 1 |
| Combat | 3.0x | 0.5x | Speed Tier 2 |
| Ace | 5.0x | 0.3x | Speed Tier 3 |
| Afterburn | 5.0x | 0.2x + boost | Speed Tier 4 |

---

## Part 6: Threat Levels and Waves

| Threat | Fighters Per Wave | Waves | How to Unlock |
|--------|------------------|-------|---------------|
| 1 | 1–2 | 1–2 | Default |
| 2 | 2–3 | 2–3 | Default |
| 3 | 3–4 | 3–4 | Discover 3+ islands |
| 4 | 4–6 | 4–5 | Discover 5+ islands |
| 5 | 6–8 | 5–6 | Discover 5+ islands |

At Threat 4+, ambient enemy encounters spawn between engagements while you're roaming.

**Combat flow:** ROAMING (fly freely, weapons active) → ENGAGEMENT (waves of enemies) → WAVE COMPLETE (scrap awarded, 10s pause) → next wave or back to ROAMING.

---

## Part 7: Flight and Power Settings

The **Flight** tab gives you direct control over aircraft performance:

| Setting | Options |
|---------|---------|
| Engine Power | 2x or 5x thrust multiplier |
| Air Resistance | Stock, Realistic Glide, Reduced, Low, Minimal |
| RPM Uncap | Remove RPM limiter |
| ALL MAX | One-button 5x power + realistic glide |
| Boost | Off, Light (2K), Medium (10K), Heavy (50K), RIDICULOUS (200K) |
| Landing Mode | Reduced power + increased control for landings |

Press **F2** for a real-time vehicle stats HUD (speed, altitude, RPM, drag, force).

---

## Part 8: Cheats (Single-Player Only)

All cheats are **automatically disabled during multiplayer sessions**. The mod detects active network connections and hard-disables these toggles during online play.

| Cheat | What It Does |
|-------|-------------|
| Unlimited Fuel | Fuel never depletes |
| Unlimited Ammo | Ammo never depletes |
| God Mode | Invulnerable + no crash damage |
| Money Editor | Adjust in-game currency ($100K, $1M, $9.9M) |
| Unlock All Vehicles | All 6 aircraft available |
| Vehicle Swap | Fly any aircraft in any mission |
| Weather Control | Day, Sunset, Night, Overcast, Auto |
| Unlock All Missions | Access every mission type |
| Disable Crashes | Turn off crash detection |
| Manual Save | Force save outside a mission |
| Dev Save (Slot 2) | Create a fully-unlocked save file |

---

## Part 9: Custom Combat Music (Optional)

1. Create the folder: `<GameDir>/UserData/HostileSkies/Music/`
2. Drop any `.ogg` audio files into it
3. In-game, use the Hostile Skies tab to:
   - Toggle between original game music and your playlist
   - Skip tracks (next/previous)
   - Adjust volume

Game BGM auto-mutes when HS music is playing.

---

## Multiplayer Safety

All cheats, sandbox features, and combat spawning are **automatically disabled in multiplayer**. The mod detects active network connections and hard-disables all gameplay-altering toggles during online sessions. No manual action needed — the mod handles this automatically.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Mod menu doesn't appear | Check that `UW2TrainerMod.dll` is in the `Mods/` folder. Check `MelonLoader/Latest.log` for errors |
| Prefab status says "NOT LOADED" | Play a combat mission first, or press "Load Enemy Prefabs" in the Hostile Skies tab |
| Enemies spawn but don't attack | Make sure Hostile Skies is activated on the floating panel |
| Weapons don't fire in free flight | Activate Hostile Skies first — weapons auto-enable with HS |
| Secondary fire (A button) doesn't work | Hold A button, don't tap. Also verify HS is activated |
| Scrap not saving | Check that `Mods/UW2Trainer_Combat.txt` is writable |
| Game crashes on Lightning aircraft | The Lightning (vehicle ID 64) is cut content and will crash — avoid it |
| MelonLoader shows errors on startup | Make sure you launched the game once after installing MelonLoader to generate assemblies |

---

## Uninstalling

1. Delete `UW2TrainerMod.dll` from the `Mods/` folder
2. (Optional) Remove MelonLoader entirely via the installer or delete the `MelonLoader/` folder

The mod makes no permanent changes to game files.
