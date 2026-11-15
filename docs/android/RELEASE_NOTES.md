# Hokkaido 0.6.5

Tested on a Samsung Galaxy S26 (Exynos 2600, Xclipse 960, 12 GB) and, for the first time, a Galaxy S25 (Snapdragon 8 Elite, Adreno 830, 12 GB), both on Android 17. The performance work tested on the S26's Exynos carries over well to Snapdragon.

## Highlights

- **Fast Fusion** now gets past its title screen and into races, but at low frame rates (the game runs in slow motion) and with a shimmering image. Before, it crashed right after the splash screen on every phone tested: at 0.5x resolution, render targets were freed while a cached scaling helper still used them.
- **Ocarina of Time on 12 GB phones:** Ocarina of Time will no longer be optimized for 12 GB devices. It needs more memory than a 12 GB phone has free and can be closed for low memory there. 16 GB of RAM is recommended.
- **Speed and memory** (upstream)
  - GPU address space is reused and given back when the allocator runs out.
  - Command list copies are reused instead of made again.
  - Occlusion query lookups, frees and locks are cheaper.
  - Game file sections open when they are first used.
  - Memory write traps skip the texture cache on pages that hold no texture.
  - Fewer GPU submissions in the middle of a draw.
- **Stability** (upstream)
  - A render target that got no memory is left out instead of crashing the driver.
  - A shader translation fix for bit-field extracts.
  - Movies of games that pace themselves no longer drop frames.
  - Converted ASTC textures are submitted to the GPU only once complete.
  - The log is written out every second, so a crash or hang keeps its last lines.
- **For contributors:** `EDEN_NX2_GPU_LIST_DUMP` shows the command lists the GPU writes for itself, which is what slows Fast Fusion down.

## Known issues

- Fast Fusion runs at low frame rates, loads slowly and its image shimmers.
- Ocarina of Time can stay on a black screen after its intro movie on some Snapdragon phones (issue #12); the S25 we test on gets past it.
- Ocarina of Time sometimes starts with graphical glitches; restarting the game helps. Use **0.5x**.
- Pokopia's sky is black.
- Microphone input is not supported on Android.
- The phone heats up during long sessions and slows down until it cools.

## For testers

- Install the APK, add your games folder, and set up keys and firmware as usual. None are included.
- Recommended: Handheld mode, NCE CPU backend, 0.5x resolution, and a custom RADV driver on Xclipse GPUs.
- Diagnostic switches can be set in `Android/data/dev.lichii.android/files/env.txt` (see the README).
- Report problems at https://github.com/pavelgajdo/Hokkaido/issues with your phone, driver and `eden_log.txt`.
