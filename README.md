# Fire Emblem Fortune's Weave Resolution Modpack

Resolution unlock patches for Fortune's Weave on Eden and Eglantine.

---

## Disclaimer

This modpack contains patch files only. It does not contain any game code, assets, encryption keys, or other copyrighted material.

You must legally own a copy of Fortune's Weave to use these patches. This project is not affiliated with, endorsed by, or sponsored by Nintendo or Intelligent Systems.

---

## Background

Fortune's Weave uses a fixed 50 percent render scale no matter what resolution the console is set to. In practice this means the game always runs in what DLSS would call Performance mode:

| Mode | Output resolution | Internal render resolution |
|------|-------------------|----------------------------|
| Docked | 1440p (2560x1440) | 720p (1280x720) |
| Handheld | 1080p (1920x1080) | 540p (960x540) |

The game then upscales that internal image to the output resolution.

## What this mod does

The patches replace both the input (render) resolution and the output resolution by patching the game's code directly. Each patch targets a specific output resolution and a specific internal render scale, so you can choose how much of the GPU budget goes to sharpness versus performance.

Supported output resolutions:

- 1080p (1920x1080)
- 1440p (2560x1440)
- 2160p (3840x2160)

Three ZIP files are provided, one per output resolution. Each ZIP contains the full set of quality levels listed below.

## Included quality levels

Every resolution ZIP includes the following modes, named after their DLSS equivalents:

| Mode | Internal render scale | Notes |
|------|-----------------------|-------|
| Native (DLAA) | 100 percent | Renders at the full output resolution, uses DLAA style anti-aliasing |
| Quality | 66 percent | Higher internal resolution, lower performance |
| Balanced | 58 percent | Middle ground |
| Performance | 50 percent | Matches the game's original behavior, but at your chosen output resolution |
| Ultra Performance | 33 percent | Lowest internal resolution, highest performance |

Each mode is its own mod folder. Enable exactly one at a time. Enabling more than one resolution or mode patch at once will cause conflicts.

---

## Requirements

- Eglantine build 219 or newer. Earlier builds had a bug that broke the game's DLSS network resulting in blurry artifacts, if you see this, make sure to update to the latest build.
- A GPU and enough system memory to handle your chosen target. See the Known Issues section for the 4K caveats.

## Docked mode

This modpack is designed for and tested in Docked mode only. The resolution patches ignore Handheld mode, so behavior there is unpredictable and untested.

Set Eden to Docked before booting:

```
Emulation > Configure > System > use_docked_mode: Docked
```

## Upscaling options

The patches control the game's render and output resolutions. Upscaling on top of that can come from either of two sources:

- The game's own DLSS implementation. This works as normal and respects the patched resolutions.
- Eglantine's NVIDIA DLSS injector. This also respects the patched resolutions, so you can use it instead of or alongside the game's DLSS.

FSR 3.1 is built into the emulator as a fallback. It also respects the patched resolutions, so it is a valid choice if you do not have an RTX card or prefer not to use the injector. **FSR 3.1 has a lower lower-bound for its upscaling resolution so you may see a black screen if the internal resolution is too low, simply go up a quality level to fix it.

---

## Installation

1. Download the ZIP for your target resolution.
2. Extract the mod folders into the following directory:

   ```
   %APPDATA%\eden\load\04007EF01F8AE000\
   ```

   On a typical Windows install this is `C:\Users\<you>\AppData\Roaming\eden\load\04007EF01F8AE000\`.
3. Open Eden and right click Fortune's Weave, then open Properties and go to the Mods tab.
4. Enable exactly one mode.
5. Boot the game in Docked mode.

---

## Known Issues

### Black screen on boot

A black screen after launching almost always means the emulator has run out of host resources, most commonly system RAM rather than VRAM. The 2160p Native mode is the heaviest option and is the most likely to trigger this on 16 GB systems.

Ways to work around it:

- Drop the quality level by one step, for example 2160p Native to 2160p Quality, or 2160p Quality to 2160p Balanced.
- Move down to the 1440p ZIP entirely.
- Increase Eden's emulated memory layout, for example from 8 GiB to 10 GiB or 12 GiB, to free host RAM for the emulator's own texture cache.

The 4K patches are genuinely demanding. 2160p Native needs a strong system to run reliably.

### Fade to black transition artifact

On some non-standard resolutions, the fade to black transition can look odd for a frame or two. The image appears to shrink or render at an incorrect size because the fade animation does not follow the resolution scale at all and is drawn at its original size.

May or may not affect gameplay or cutscenes, further testing is required

---

## Tested configuration

- Eglantine build 219 or newer
- Docked mode
- NVIDIA GPU (RTX 3060, 12GB VRAM)
- 16 GB system RAM

Other configurations will work, but results at 2160p Native in particular depend heavily on available memory and GPU headroom.

---

## Feedback

If you run into problems, please include the following in your report. The black screen issue in particular depends on system resources, and this information makes it much easier to diagnose:

- Target resolution and quality mode
- Eglantine build number
- GPU model
- System RAM
- Your eden log file
