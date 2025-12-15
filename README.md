# DayZ-AutomationZ-Uploader-FTP-Tool
This tool uploads preset files to your DayZ server via FTP/FTPS. It is NOT a DayZ mod and is NOT added to server parameters.
[![Day-Z-Automation-Z-(1).png](https://i.postimg.cc/cC0H7Jh0/Day-Z-Automation-Z-(1).png)](https://postimg.cc/PpVTTT0R)

## Short Introduction
DayZ AutomationZ Uploader is a lightweight, server-side automation tool designed to make managing configuration files across one or many servers fast, safe, and repeatable.  
It uploads predefined local files to remote servers via FTP or FTPS — no mods, no server parameters, and no in-game dependencies required.

Although originally created for DayZ servers, the tool is **not limited to games**. It can be used for **any server or service** that relies on FTP-accessible configuration files.

---

## Why AutomationZ Exists
As a server owner, there are moments where you *must* update server files but *cannot* be online:
- weekend raid windows
- scheduled config switches
- notification rotations
- loadout changes
- rule changes
- maintenance while away or offline

Doing this manually means:
- logging in remotely
- navigating FTP directories
- overwriting the wrong file by accident
- forgetting to restore backups

AutomationZ was created to remove that friction.

The goal:
- **prepare once**
- **switch instantly**
- **avoid mistakes**
- **reduce admin presence requirements**

---

## Core Concept (How It Works)
AutomationZ is built around three simple concepts:

### 1. Profiles
Profiles store FTP/FTPS connection details:
- host
- port
- username
- password
- protocol (FTP or FTPS)
- server root directory

You can add **as many profiles as you want**.
This makes AutomationZ ideal for:
- owners with multiple game servers
- communities with test / staging / live servers
- people managing servers for friends or clients

Switching servers is as simple as selecting another profile.

---

### 2. Presets
A preset is just a local folder containing files you want to upload.

Example:
```
presets/
 ├─ raid_on/
 │   ├─ BBP_Raid_on.json
 │   └─ BBP_Raid_on_2.json (just a example, whatever you name the files it will only fill the content of the file in the remote path.)

        (So BBP_Raid_on.json or BBP_Raid_on_2.json will write its contents to BBP_Settings.json and optionally
        creates a backup before upload, it will never rename the file or create a new copy unless you made a typo somewhere.
        then it simply creates a new file. So double check the file name in the remote path at mappings! Its case sensitive.
        Path and file need to match exactly.
        This way you can make multiple loadouts like 1 for each day or multiple Messages / notification in game for each day etc.)
 ├─ raid_off/
 │   ├─ BBP_Raid_off.json
 │   └─ BBP_Raid_off_2.json
```

You select **one preset at a time**.
All uploads use files from that preset folder only.

---

### 3. Mappings
Mappings define **what goes where**.

Each mapping contains:
- a local file name (inside the preset)
- a remote target path (on the server)
- optional backup-before-overwrite

Example:
```
Local:  BBP_Raid_on.json
Remote: config/BaseBuildingPlus/BBP_Settings.json
```

Different local filenames can overwrite the **same remote file**, allowing clean mode switching without renaming files on the server.

Mappings can be:
- enabled or disabled individually
- reused across multiple servers
- shared across presets

---

## Backup Safety
Before overwriting any remote file, AutomationZ can automatically:
- download the existing server file
- store it locally with timestamped folders

Backup structure:
```
backups/<profile>/<preset>/<timestamp>/
```

This allows instant rollback if something goes wrong.

---

## Why This Is Especially Useful for Game Server Owners
For game servers (DayZ, or any other):
- no workshop mods required
- no client downloads
- no server restarts needed beyond what you already control
- no admin being online at the exact moment

Typical use cases:
- enable/disable raids
- rotate messages.xml
- switch Expansion notification schedules
- change economy or gameplay configs
- manage test vs live environments

You prepare everything **once**, then upload in seconds.

---

## Not Just for Game Servers
AutomationZ is intentionally generic.

It works for:
- web servers
- voice servers
- automation scripts
- configuration-based services
- any FTP-accessible environment

If you can upload a file via FTP, AutomationZ can manage it.

---

## What AutomationZ Is NOT
- ❌ It is NOT a DayZ mod
- ❌ It is NOT added to server startup parameters
- ❌ It does NOT modify gameplay code
- ❌ It does NOT require players to download anything

It is a **pure external automation tool**.

---

## Design Philosophy
- simple UI
- no unnecessary features
- explicit control
- predictable behavior
- human-error prevention

The tool is intentionally boring — and that is a feature.

---

## Status
This project is actively used in production environments.
Windows and Linux are confirmed working.
macOS should work with Python 3 + Tk installed.

---

## Author
Created by **Danny van den Brande**  
Built for server owners who value control, safety, and their free time.

## License
This project is licensed under the MIT License.
