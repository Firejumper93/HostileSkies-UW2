# Hostile Skies — Setup Guide

Complete setup instructions for installing and running the Hostile Skies mod for Ultrawings 2.

---

## Prerequisites

- **Ultrawings 2** installed (PC VR — Oculus or Steam)
- A VR headset (Quest via Link/Air Link, Rift, Index, etc.)

---

## Part 1: Install MelonLoader

MelonLoader is the mod framework that lets Hostile Skies run inside UW2.

1. Download **MelonLoader Installer** from https://github.com/LavaGang/MelonLoader/releases
   - Get `MelonLoader.Installer.exe` (latest v0.5.x – v0.7.x all work)
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
1. Download `UW2TrainerMod.dll` from the [Releases](https://github.com/Firejumper93/HostileSkies-UW2/releases) page (or the `bin/Debug/` folder in the repo)
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
4. You should see the Hostile Skies menu with 8 tabs: Cheats, Flight, Combat, Physics, Aircraft, Explore, Info, Diag

If the menu doesn't appear, check `MelonLoader/Latest.log` for errors.

---

## Part 4: Activating Hostile Skies (Combat Mode)

This is the most important part. Enemy fighters don't exist in free flight by default — the mod needs to grab them from a combat mission first.

### First Time Setup (Once Per Session)

1. From your office, fly to any island
2. Start **any combat mission** — Dogfight, Target Elimination, Air Defense, etc.
3. Wait a few seconds for the mission to load
4. The mod automatically detects and caches all enemy prefabs in the background
5. You can quit the mission immediately or finish it — either way the prefabs are saved
6. Return to free flight

> The mod saves the combat scene name to `Mods/UW2Trainer_Combat.txt`. On future sessions, you can load prefabs directly from the **Combat** tab without replaying a mission.

### Activating Combat

1. In free flight, press **Spacebar/F1** to open the mod menu
2. Go to the **Combat** tab
3. Verify prefab status shows **READY** (green) for Messer and/or Wolf
4. Press **"Activate Hostile Skies"** on the floating panel
5. Choose your battle:
   - **Spawn 1 Enemy Fighter** — single bandit
   - **Skirmish** — 2 enemies
   - **Small Battle** — 4 enemies
   - **Invasion** — 8 enemies
   - **All Out War** — 15 enemies
6. Close the menu and fight!

### Combat Controls

| Input | Action |
|-------|--------|
| **Right Trigger** | Fire primary weapon |
| **A Button (hold)** | Fire secondary weapon (grenades/bombs, 1.2s cooldown) |
| **Spacebar / F1** | Open menu to spawn more enemies or adjust settings |

### What You'll See

- Enemy fighters spawn near your position and immediately turn to attack
- Your cockpit EFI screen shows **kill count**, **wave number**, and **"ATTACKERS DETECTED"** alerts
- An alert bell sounds when new enemies spawn
- Your weapons auto-enable when Hostile Skies is active

> **If your weapons aren't firing:** Make sure you pressed "Activate Hostile Skies" on the floating panel first. The weapons system requires HS to be toggled on.

---

## Part 5: Custom Combat Music (Optional)

1. Create the folder: `<GameDir>/UserData/HostileSkies/Music/`
2. Drop any `.ogg` audio files into it
3. In-game, use the **Combat** tab to:
   - Toggle between original game music and Hostile Skies playlist
   - Skip tracks (next/previous)
   - Adjust volume

The game's background music auto-mutes when HS music is playing.

---

## Multiplayer Safety

All sandbox and combat features are **automatically disabled in multiplayer**. The mod detects active Photon network connections and hard-disables all gameplay-altering toggles during online sessions. You do not need to manually turn anything off — the mod handles this automatically to ensure fair play.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Mod menu doesn't appear | Check that `UW2TrainerMod.dll` is in the `Mods/` folder. Check `MelonLoader/Latest.log` for errors |
| Prefab status says "NOT LOADED" | You need to play a combat mission first to cache enemy prefabs |
| Enemies spawn but don't attack | Make sure Hostile Skies is activated on the floating panel |
| Weapons don't fire in free flight | Activate Hostile Skies first — weapons auto-enable with HS |
| Secondary fire (A button) doesn't work | Hold A button, don't tap. Also verify HS is activated |
| Game crashes on Lightning aircraft | The Lightning (vehicle ID 64) is cut content and will crash — avoid it |
| MelonLoader console shows errors | Make sure you launched the game once after installing MelonLoader to generate assemblies |

---

## Uninstalling

1. Delete `UW2TrainerMod.dll` from the `Mods/` folder
2. (Optional) Remove MelonLoader entirely by running the installer and choosing Uninstall, or delete the `MelonLoader/` folder

The mod makes no permanent changes to game files.
