> [!Note]
> PixelFlow is now archived and no longer maintained. For continued maintenance and development, a community-driven spin-off led by one of the core contributors is available here: https://github.com/EtienneLescot/pixelflow


> [!WARNING]
> This started as a side project that blew up; not production grade and you'll hit bugs, but hopefully it covers what you need. **This project will soon be archived.**


<p align="center">
  <img src="public/pixelflow.png" alt="PixelFlow Logo" width="64" />
  <br />
  <br />
	<a href="https://trendshift.io/repositories/17427" target="_blank"><img src="https://trendshift.io/api/badge/repositories/17427" alt="AshishUjjwal%2Fpixelflow | Trendshift" style="width: 256px; height: 64px;" width="256" height="64"/></a>


  </a>
</p>

# <p align="center">PixelFlow</p>

<p align="center"><strong>PixelFlow is a modern screen recording and visual capture tool designed to create smooth, professional recordings with real-time cursor movement tracking.</strong></p>

It captures screen activity while highlighting cursor interactions, making it ideal for tutorials, product demonstrations, technical walkthroughs, presentations, and UI showcases.

**100% free** for both **personal** and **commercial** use. Use it, modify it, distribute it. Please respect the License. 

> [!NOTE]
>Software should be accessible. PixelFlow has no paid tiers, premium features, upsells, or functionality locked behind a paywall.

<p align="center">
	<img src="public/demo.png" alt="" style="height: 0.2467; margin-right: 12px;" />
  <img src="public/sample.png" alt="" style="height: 0.2467; margin-right: 12px;" />
</p>

## Core Features
- Record a specific window, or your whole screen.
- Record microphone and system audio.
- Webcam overlay with picture-in-picture, drag-to-position, mirroring, and shape options.
- Auto or manual zooms with adjustable depth, duration, easing, and pixel-precise position; auto-zoom follows your cursor as you work.
- Custom cursor size, smoothing, and click effects, with cursor themes and post-recording path smoothing.
- Automatic captions for voiceovers, generated on-device with no upload (works offline).
- Wallpapers, solid colors, gradients, or your own background image.
- Motion blur.
- Crop, trim, and per-segment speed control on the timeline.
- Text, arrow, and image annotations, with text animation presets.
- Timeline snapping guides and an audio waveform to make trimming easier.
- Customizable keyboard shortcuts.
- Export to MP4 or GIF in multiple aspect ratios and resolutions.
- Languages supported: Arabic, English, Spanish, French, Italian, Japanese, Korean, Portuguese (Brazil), Russian, Turkish, Vietnamese, Simplified Chinese, and Traditional Chinese.


## Installation

Download the latest installer for your platform from the [GitHub Releases](https://github.com/AshishUjjwal/pixelflow/releases) page.

### macOS

The easiest way to install on macOS is via [Homebrew](https://brew.sh):

```bash
brew install --cask AshishUjjwal/pixelflow/pixelflow
```

Brew automatically picks the right build for Apple Silicon or Intel, and verifies the download against a notarized signature so Gatekeeper won't block it.

To update later: `brew upgrade --cask pixelflow`
To uninstall: `brew uninstall --cask pixelflow` (add `--zap` to also remove app data)

#### Manual install (if you prefer)

If you'd rather grab the `.dmg` directly from the [Releases page](https://github.com/AshishUjjwal/pixelflow/releases) and encounter Gatekeeper blocking the app, you can bypass it by running the following command in your terminal after installation:

```bash
xattr -rd com.apple.quarantine /Applications/Pixelflow.app
```

Note: Give your terminal Full Disk Access in **System Settings > Privacy & Security** to grant you access and then run the above command.

After running this command, proceed to **System Preferences > Security & Privacy** to grant the necessary permissions for "screen recording" and "accessibility". Once permissions are granted, you can launch the app.

> [!NOTE]
> **Upgrading from an older version and hitting permission issues?** If you already had PixelFlow installed and the new version won't record (Screen Recording or Accessibility keep failing even after you grant them), uninstall the old version, remove PixelFlow's existing entries under **System Settings > Privacy & Security** (both Screen Recording and Accessibility), then do a fresh install and grant the permissions again when prompted.

### Windows

Install via [winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/):

```bash
winget install AshishUjjwal.PixelFlow
```

To update later: `winget upgrade AshishUjjwal.PixelFlow`
To uninstall: `winget uninstall AshishUjjwal.PixelFlow`

If you'd rather grab the `.exe` installer directly, download it from the [Releases page](https://github.com/AshishUjjwal/pixelflow/releases).

### Linux

Three packages are published to the [Releases page](https://github.com/AshishUjjwal/pixelflow/releases) for each version. Pick the one that matches your distro:

**Debian / Ubuntu / Pop!_OS (`.deb`)**
```bash
sudo apt install ./Pixelflow-Linux-latest.deb
```

**Arch / Manjaro (`.pacman`)**
```bash
sudo pacman -U Pixelflow-Linux-latest.pacman
```

**Any distro (`.AppImage`)**
```bash
chmod +x Pixelflow-Linux-*.AppImage
./Pixelflow-Linux-*.AppImage
```

**NixOS / Nix (flake)**

Try without installing:
```bash
nix run github:AshishUjjwal/pixelflow
```

Install into your user profile:
```bash
nix profile install github:AshishUjjwal/pixelflow
```

For a NixOS system config (flake):
```nix
{
  inputs.pixelflow.url = "github:AshishUjjwal/pixelflow";

  outputs = { nixpkgs, pixelflow, ... }: {
    nixosConfigurations.<host> = nixpkgs.lib.nixosSystem {
      modules = [
        pixelflow.nixosModules.default
        { programs.pixelflow.enable = true; }
      ];
    };
  };
}
```

For Home Manager, use `pixelflow.homeManagerModules.default` with the same `programs.pixelflow.enable = true;`.

You may need to grant screen recording permissions depending on your desktop environment.

**Sandbox error:** If the AppImage fails to launch with a "sandbox" error, run it with `--no-sandbox`:
```bash
./Pixelflow-Linux-*.AppImage --no-sandbox
```

### Platform differences

Everything in the editor and export is the same on macOS, Windows, and Linux: zooms, backgrounds, motion blur, crop/trim/speed, blur regions, annotations, auto-captions, projects, export, and all languages. The differences are in **capture**, where macOS and Windows use a native pipeline that Linux doesn't have:

- **Native recording**: macOS (ScreenCaptureKit) and Windows (Windows Graphics Capture) record through a native pipeline for higher quality and clean window-level capture. Linux records through the browser pipeline instead.
- **Custom cursors**: on macOS and Windows the real cursor is captured (shape, type, and clicks), which powers the cursor themes, click effects, and editable cursor overlay. On Linux only the cursor position is captured (used for auto-zoom), so those cursor options aren't available.
- **Webcam**: captured natively on macOS and Windows; on Linux it's recorded through the browser, but still works as a picture-in-picture overlay.
- **System audio** support varies by OS:
  - **macOS**: requires macOS 13+. On macOS 14.2+ you'll be prompted to grant audio capture permission. macOS 12 and below can't capture system audio (mic still works).
  - **Windows**: works out of the box.
  - **Linux**: needs PipeWire (default on Ubuntu 22.04+, Fedora 34+). Older PulseAudio-only setups may not capture system audio (mic should still work).

---

## License

This project is licensed under the [MIT License](./LICENSE). By using this software, you agree that the authors are not liable for any issues, damages, or claims arising from its use.
