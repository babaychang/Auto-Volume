# Auto Volume for OBS Studio

**Auto Volume** is a native OBS Studio plugin by **Babay Chang**. It adds an
**Tools > Auto Volume** window for configuring audio levels and fade behavior
per scene.

> **Compatibility:** OBS Studio 33.0.0, Windows 64-bit.

## Features

- Save a separate volume profile and fade settings for each scene.
- List audio sources in the selected scene, including sources inside groups and
  nested scenes.
- Set a source level with a slider or enter a percentage from 0% to 100%.
- Apply the selected scene's audio profile when the active scene changes.
- Choose a fade style per scene:
  - **Normal Fade** — smooth, eased volume changes.
  - **Linear Fade** — volume changes at a constant rate.
  - **Crossfade** — attempts to fade out sources found only in the outgoing
    scene while fading in sources found only in the incoming scene.
- Set a per-scene delay in milliseconds before a scene-change fade begins.
- Configure an optional Start Fade level independently for each audio source.
- Export and import volume profiles and fade settings as JSON files.
- Reset a selected scene's audio levels and fade settings to their defaults.
- Display English help text when hovering over controls and table columns.

## Important notes

OBS controls the mixer volume of a source, not a separate copy of that source
for every scene. When a source is shared by multiple scenes, Auto Volume applies
the profile for the currently active scene to that shared source. It does not
duplicate sources or provide independent simultaneous mixer levels for the
same source.

Start Fade is configured per source. Choose a source from the **Audio Source**
dropdown beside the Start Fade percentage; changing one source's setting does
not change the Start Fade settings of other sources in that scene.

Fade styles are used when the active scene changes. Adjusting a volume slider
or entering a percentage applies that value directly and does not demonstrate
the fade curve.

Crossfade depends on the outgoing source remaining active long enough for its
volume to fade. OBS may stop or hide sources as part of a scene transition, so
an outgoing fade is not guaranteed to be audible in every OBS setup. A source
used by both scenes is treated as the same shared source and is not crossfaded
against itself.

## Install a prebuilt plugin

1. Download and extract the complete plugin ZIP.
2. Copy the `Install\auto-volume` folder into:

   ```text
   C:\ProgramData\obs-studio\plugins
   ```

   The installed file should be:

   ```text
   C:\ProgramData\obs-studio\plugins\auto-volume\auto-volume.dll
   ```

3. If Windows requests permission, approve the copy.
4. Restart OBS and open **Tools > Auto Volume**.

Close OBS before replacing or removing the DLL. A DLL-only ZIP is also
available; place its `auto-volume.dll` in the same plugin folder shown above.

## Use the plugin

1. Open **Tools > Auto Volume**.
2. Use **Save Profile** or **Load Profile** in the upper-right corner to
   export or import a JSON profile.
3. Choose a scene from **Select Scenes**. The **Audio Source** table shows
   sources in that scene, including sources in groups and nested scenes.
4. Set each source's level using the slider or the **Volume (%)** field.
   The percentage field supports typing and copy/paste (including pasted values
   with a trailing `%`). Press **Ctrl+C** in the field to copy its percentage.
   The allowed range is 0% to 100%.
5. Set the fade options for the selected scene:

   | Setting | Description |
   | --- | --- |
   | **Start Fade (%)** | Select an **Audio Source**, then enable Start Fade and set that source's 0%–100% starting volume. Each source has its own setting. The field supports typing and copy/paste, including a trailing `%`; press **Ctrl+C** to copy. Disabled by default; it does not affect manual slider edits. |
   | **Fade Duration (s)** | Base duration for a full-range volume change, shown with the `s` unit. A change from 0% to 100% uses the full duration. Set to 0 for an immediate change. |
   | **Fade minimum (s)** | Minimum duration, shown with the `s` unit, used for smaller changes, capped at Fade Duration. |
   | **Fade Short Length (%)** | Extends the duration of smaller volume changes. Its value is shown as a percentage. It has no effect on a full 0%-to-100% change and may be masked by Fade minimum. |
   | **Fade Style** | Selects Normal Fade, Linear Fade, or Crossfade for scene transitions. |
   | **Delay (ms)** | Wait time before the selected scene's volume transition starts. The default is 0 ms; the value can be set from 0 to 60,000 ms. It does not delay manual slider or percentage edits. |

6. Repeat for other scenes. Profiles and fade settings are saved per scene and
   scene collection.
7. Enable **Active Auto** to apply profiles automatically when the active
   scene changes. When disabled, you can still edit profiles, but the plugin
   will not automatically apply them to the mixer.

### Save and load JSON profiles

**Save Profile** exports saved source levels and fade settings, including their
scene-collection and scene names, to a `.json` file. **Load Profile** validates
the file before applying it.

Loading uses merge behavior: imported source levels update matching
collection/scene/source entries, imported fade settings update matching
scenes, and imported Start Fade settings update matching
collection/scene/source entries. Existing entries not present in the file are
kept. Default fade settings are updated from the file. The **Active Auto** checkbox is not
included in the profile and is not changed. If the imported profile affects
the currently active scene while Active Auto is enabled, its audio profile is
applied immediately, respecting that scene's **Delay (ms)**.

### Reset scene settings

Choose a scene and click **Reset Scene to Default Settings**. This resets that
scene's audio levels to 100% and its fade settings to:

- Fade Duration: 60 seconds
- Fade minimum: 6 seconds
- Fade Short Length: 75%
- Fade Style: Normal Fade
- Delay: 0 ms
- Start Fade: disabled (0%) for each source

The **Active Auto** checkbox is not changed by the reset.

## Build from source

### Requirements

- Windows 64-bit
- Visual Studio 2022 Build Tools with **Desktop development with C++**
- Windows SDK 10.0.22621
- CMake 3.28–3.30
- Internet access for the initial CMake configuration and dependency setup

The project uses the OBS Studio 33.0.0 source and the OBS Windows and Qt 6
dependency packages. CMake downloads and verifies the configured dependency
archives; a separate manual OBS SDK installation is not required.

##

<img width="208" height="201" alt="Screenshot 2026-10-28 013720" src="https://github.com/user-attachments/assets/2f860bab-6962-4c43-a988-0056deba320c" />


## Overview

<img width="647" height="610" alt="image" src="https://github.com/user-attachments/assets/b96848f7-151f-4909-b2d7-1b4f60f83089" />


## License and attribution

Created by **Babay Chang**.

© 2026 Babay Chang All rights Reserved.







