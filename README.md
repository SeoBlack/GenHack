# 🎮 GenyV2 (GENHACK v2)

**GENHACK v2 by Sorin** — A small Windows program that adds cheats to **GeneralsOnline** (Command & Conquer: Generals Zero Hour).  
You run it while the game is open, pick options with the keyboard, and it changes things like money, XP, and radar in the game.

---

## 📑 Table of Contents

- [What does it do?](#-what-does-it-do)
- [What can I do with it?](#-what-can-i-do-with-it)
- [What do I need?](#-what-do-i-need)
- [How do I build it?](#-how-do-i-build-it)
- [How do I use it?](#-how-do-i-use-it)
- [Changing settings](#-changing-settings)
- [Project files (for developers)](#-project-files-for-developers)
- [How it works (technical)](#-how-it-works-technical)
- [⚠️ Disclaimer](#️-disclaimer)

---

## 🤔 What does it do?

GenyV2 is a **console app** (a window with text, not buttons). It:

1. **Finds your game** — It looks for the GeneralsOnline window by its title.
2. **Connects to it** — It opens the game’s process so it can read and write its memory.
3. **Lets you turn cheats on/off** — You press **F1–F6** to toggle each option. A checkmark **[X]** means it’s on.

**Controls:**

- **F1–F6** — Turn an option ON or OFF  
- **ESC** — Close the program (the game keeps running)

That’s it. No need to click ENTER to “confirm” — just press the F-key to toggle.

---

## ✨ What can I do with it?

### 🕹️ Single-Player

| Key | Option | What it does |
|-----|--------|----------------|
| **F1** | 💰 Hack Money 1000000+ | Adds 1,000,000 to your current money. |
| **F2** | ⭐ Get 5000 XP | Sets your XP to 5000. |
| **F3** | 🌟 Get 20 Stars | Sets your Stars to 20. |
| **F4** | ⚡ Instant Special Power Recharge | Special weapons and upgrades recharge instantly (no waiting). |

### 🌐 Multiplayer

| Key | Option | What it does |
|-----|--------|----------------|
| **F5** | 📡 Radar Hack | Reveals the minimap (simple version). |
| **F6** | 📡 Advanced Radar Hack | Shows units and buildings on radar. **Turn this ON before the match starts** for best results. |

**Tip:** You can turn options **on and off** anytime. When you turn off radar or special power, the program puts the game code back to normal.

---

## 📋 What do I need?

Before you start, make sure you have:

| What | Details |
|------|---------|
| 🖥️ **Windows** | Any recent Windows (32-bit or 64-bit is fine). |
| 🔧 **Visual Studio** | You need this only to **build** the project. Use Visual Studio 2022 (or 2019) with “Desktop development with C++” installed. |
| 🎮 **The game** | GeneralsOnline — the one that runs as `GeneralsOnlineZH_60.exe` with the window title that contains “GeneralsOnline ~2075” and “GitHub Buildserver”. |
| 🔐 **Admin (sometimes)** | If the game was started as Administrator, run GenyV2.exe as Administrator too. |

---

## 🔨 How do I build it?

**Building** means turning the source code into an `.exe` file you can run.

1. **Open the project**  
   Double-click **GenyV2.slnx** (or open it from Visual Studio).

2. **Pick how to build**  
   At the top of Visual Studio, choose:
   - **Release** (recommended) or Debug  
   - **x64** (recommended) or Win32  

3. **Build**  
   Press **Ctrl+Shift+B** or use the menu: **Build → Build Solution**.

4. **Find your program**  
   When it’s done, the `.exe` is here:  
   `GenyV2\x64\Release\GenyV2.exe`  
   (If you chose Debug or Win32, the path will say Debug or Win32 instead.)

**💡 Icon note:** The project expects an icon file (e.g. `logo.ico`). If you get an error about a missing icon, you can edit **GenyV2.rc** and point it to an icon you have, or remove the icon line. The program will still build and run.

---

## 🚀 How do I use it?

1. **Start the game** (GeneralsOnline) and leave it open.
2. **Run GenyV2.exe**  
   If the game is running as Administrator, run GenyV2.exe as Administrator too (right‑click → Run as administrator).
3. **Use the menu**  
   - Press **F1** to add money, **F2** for XP, **F3** for stars, etc.  
   - **[X]** = option is ON, **[ ]** = option is OFF.  
   - Press the same F-key again to turn an option off (where that applies).
4. **When you’re done**  
   Press **ESC** to close GenyV2. The game keeps running. Any cheats you left ON stay active until you turn them off or close the game.

**❓ “Process not found” or “Failed to get module base address”**  
- Make sure the game is actually running.  
- The game window title must match exactly what the program expects (the GeneralsOnline ~2075 GitHub Buildserver version).  
- The exe must be `GeneralsOnlineZH_60.exe`.

---

## ⚙️ Changing settings

All the numbers and names the program uses (game title, how much money to add, etc.) are in one place:

- **File:** `GenyV2/Config.cpp`  
- **Declarations:** `GenyV2/Config.h`

If you use a **different version** of the game, you may need to change:

| What you want to change | Variables to look at |
|-------------------------|----------------------|
| Game process / window name | `PROCESS_NAME`, `WINDOW_TITLE` |
| Money amount | `MONEY_CHEAT_AMOUNT`, and money/player offsets |
| XP / Stars amount | `XP_CHEAT_AMOUNT`, `STARS_CHEAT_AMOUNT`, and their offsets |
| Radar (simple) | `SIMPLE_RADAR_OFFSET` |
| Radar (advanced) | `ADVANCED_RADAR_OFFSET_1`, `ADVANCED_RADAR_OFFSET_2` |
| Special power patch | `SPECIAL_POWER_OFFSET`, `SPECIAL_UPGRADES_OFFSET` |

After editing, **build the project again** (Ctrl+Shift+B) so the changes are in the new `.exe`.

---

## 📁 Project files (for developers)

If you want to understand or change the code, here’s what the main files do:

```
GenyV2/
├── GenyV2.slnx          ← Solution (open this in Visual Studio)
├── README.md             ← This file
└── GenyV2/
    ├── GenyV2.vcxproj   ← Project settings (build config, etc.)
    ├── GenyV2.cpp       ← Main program: menu, keyboard (F1–F6, ESC)
    ├── GenyV2.h
    ├── Config.cpp       ← All settings: game name, offsets, cheat amounts
    ├── Config.h
    ├── MemoryManager.cpp ← Finds game, reads/writes memory, applies patches
    ├── MemoryManager.h
    ├── resource.h
    └── GenyV2.rc        ← App icon (path to .ico)
```

- **Config** = game name, window title, and all the numbers (offsets, amounts). Change these to support another game build.
- **MemoryManager** = finding the process, getting the game’s base address, following pointers, and writing bytes (patches and values).

---

## 🔧 How it works (technical)

Optional read — only if you care about the implementation:

- **Finding the game:** Uses the window title to get the window → then gets the process ID → opens the process with `OpenProcess`.
- **Game base address:** Uses a snapshot of the process modules to find `GeneralsOnlineZH_60.exe` and its base address.
- **Player data (money, XP, stars):** Follows a pointer chain from a fixed address to the “player” structure, then uses offsets for money, XP, and stars.
- **Patches (radar, special power):** Changes memory protection with `VirtualProtectEx`, writes new bytes with `WriteProcessMemory`, then restores the original protection. When you disable a cheat, it writes the original bytes back.

---

## ⚠️ Disclaimer

This project is for **learning and single-player / private use** only.

- Modifying a game’s memory can **break the game’s rules** or **terms of service**.
- Using such tools on **online servers** may get you **banned**.
- Use at your **own risk**. The authors are not responsible for any bans or other consequences.
- Prefer using these features **only offline** or where the game/server explicitly allows it.

---

## 📄 License

See the repository for license information. If nothing is specified, assume all rights reserved.
