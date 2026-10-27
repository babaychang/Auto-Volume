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
- Export and import volume profiles and fade settings as JSON files.
- Reset a selected scene's audio levels and fade settings to their defaults.

## Important notes

OBS controls the mixer volume of a source, not a separate copy of that source
for every scene. When a source is shared by multiple scenes, Auto Volume applies
the profile for the currently active scene to that shared source. It does not
duplicate sources or provide independent simultaneous mixer levels for the
same source.

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
   The allowed range is 0% to 100%.
5. Set the fade options for the selected scene:

   | Setting | Description |
   | --- | --- |
   | **Fade Duration (s)** | Base duration for a full-range volume change. A change from 0% to 100% uses the full duration. Set to 0 for an immediate change. |
   | **Fade minimum (s)** | Minimum duration used for smaller changes, capped at Fade Duration. |
   | **Fade Short Length (%)** | Extends the duration of smaller volume changes. It has no effect on a full 0%-to-100% change and may be masked by Fade minimum. |
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
collection/scene/source entries, and imported fade settings update matching
scenes. Existing entries not present in the file are kept. Default fade
settings are updated from the file. The **Active Auto** checkbox is not
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

The **Active Auto** checkbox is not changed by the reset.

## Build from source

### Requirements

- Windows 64-bit
- OBS Studio 33.0.0

Note: 

The project uses the OBS Studio 33.0.0 source and the OBS Windows and Qt 6
dependency packages. CMake downloads and verifies the configured dependency
archives; a separate manual OBS SDK installation is not required.

##

<img width="189" height="204" alt="image" src="https://github.com/user-attachments/assets/c4660a81-a8b4-4b1f-a4cc-364464f49f24" />

## Overview

<img width="650" height="576" alt="image" src="https://github.com/user-attachments/assets/f3a10a1c-50a1-42db-ad6f-02d383316769" />

## License and attribution

Created by **Babay Chang**.

© 2026 Babay Chang All rights Reserved.







