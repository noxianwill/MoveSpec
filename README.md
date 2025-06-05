# MoveSpec Plugin for Counter-Strike 2

## Description
MoveSpec is a CounterStrikeSharp plugin for CS2 that allows server admins to:
- Move all players to spectators
- Set team captains for T and CT
- Run a menu-driven player picking process (like a 5v5 pug system)
- Ensure fair and transparent team selection

## Features
- **Admin-only commands** for all actions
- **Menu-driven picking**: Captains take turns picking players from the spectator pool
- **Automatic team assignment**: Picked players are moved to the correct team
- **Chat announcements** for all actions and errors
- **Safe and modern**: Uses MenuManager API and PlayerSettings for compatibility

## Requirements
- CounterStrikeSharp (latest stable version)
- MenuManagerCS2 plugin (MenuManager [Core] and MenuManagerApi.dll)
- PlayerSettingsCS2 plugin (PlayerSettings [Core] and PlayerSettingsApi.dll)

> **Note:** These dependencies must be installed and working on your server. See their respective documentation for installation instructions.
**Reference:** [MenuManagerCS2](https://github.com/NickFox007/MenuManagerCS2) and [PlayerSettingsCS2](https://github.com/NickFox007/PlayerSettingsCS2)

## Installation
1. **Build the plugin** (or use a prebuilt release):
   - Place `CounterStrikeSharp.API.dll`, `MenuManagerApi.dll`, and `PlayerSettingsApi.dll` in a `3rdparty` folder in your project for building.
2. **Copy the following files from your build output (`bin/Debug/net8.0/`) to your server:**
   - `MoveSpec.dll`
   - `MoveSpec.deps.json`
   - `MoveSpec.runtimeconfig.json` (if present)
3. **Upload these files to:**
   ```
   /game/csgo/addons/counterstrikesharp/plugins/MoveSpec/
   ```
4. **Restart your server.**

## Usage
### Admin Commands
- `css_tcapt <player name>` - `!tcapt <player name>`
  - Sets the Terrorist (T) team captain and moves them to the T team.
- `css_ctcapt <player name>` - `!ctcapt <player name>`
  - Sets the Counter-Terrorist (CT) team captain and moves them to the CT team.
- `css_spec` - `!spec`
  - Moves all players (except the two captains) to spectator and starts the team picking process.
  - **Note:** Both captains must be set before using this command.
- `css_mscancel` - `!cancel`
  - Cancels the current picking process.
  - Moves all spectators back to teams (alternating between T and CT).
  - Resets all plugin state (captains, picking progress, etc.).
  - Only works when a picking process is in progress.

### Picking Process
1. Set both team captains using `!tcapt` and `!ctcapt`
2. Use `!spec` to start the picking process
3. The picking process begins, with the CT captain picking first
4. A menu is shown to the current captain, listing all available players in spectator
5. The captain selects a player from the menu; that player is moved to the captain's team
6. Turns alternate between CT and T captains
7. This continues until 8 players are picked (4 for each team), resulting in two teams of 5 (including the captains)
8. If needed, use `!cancel` to stop the process and reset everything

## Permissions
- Only players with the `@css/admin` permission can use the commands.

## Troubleshooting
- Make sure all dependencies are installed and loaded (check with `css_plugins list`).
- If you see errors about missing dependencies, double-check your server's plugin folders.
- If you see errors about permissions, make sure your admin group is set up correctly in CounterStrikeSharp.
- If `!spec` doesn't work, make sure both captains are set first.

## Credits
- Plugin by NoxianWill
- Built for CounterStrikeSharp and CS2
- Credits: [MenuManagerCS2](https://github.com/NickFox007/MenuManagerCS2) and [PlayerSettingsCS2](https://github.com/NickFox007/PlayerSettingsCS2)

---

For questions, bug report, or support, feel free to open an issue in this repository.
