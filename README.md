# MakerBridge 1.1.4 Beta — now for Mac and Windows

A local app for Mac and Windows for converting editable 3MF projects in both directions: **MakerWorld / Bambu Studio ↔ Snapmaker U1**. The current version appears beside the app name and in About MakerBridge.

**Free beta software · Developed by Brian Mayes.** Feedback and bug reports: [brian_mayes@me.com](mailto:brian_mayes@me.com). Please include your MakerBridge version, macOS or Windows version, slicer version, printer/nozzle choice and any error message.

## Download and updates

MakerBridge is free to download and use. Get the app from [Releases](https://github.com/brianmayes/MakerBridge/releases). **No GitHub account, sign-in or invitation is needed to download.** The public repository is [brianmayes/MakerBridge](https://github.com/brianmayes/MakerBridge). Under the release's **Assets**, download:

- **Mac:** `MakerBridge-Mac.zip`
- **Windows:** `MakerBridge-Windows-Setup.exe` (recommended), or `MakerBridge-Windows-Portable.zip` if you'd rather not install anything

Ignore GitHub’s automatically generated **Source code** archives; they don’t contain the app.

To share with testers, send the [Releases page](https://github.com/brianmayes/MakerBridge/releases) so they see the experimental warning and installation instructions. For future release notifications, testers with a GitHub account can select **Watch → Custom → Releases** on the repository and save. Testers without accounts can check the Releases page for updates.

To update on a Mac, quit MakerBridge, download the new release ZIP, unzip it and replace the old app. On Windows, run the new `MakerBridge-Windows-Setup.exe`; it updates the installed copy. The app does not yet download or install updates automatically.

## What's new in 1.1.4

- **MakerBridge for Windows** (Windows 10/11, 64-bit), with the same converter and options as the Mac app in both directions.
- The Windows installer is per-user (no administrator prompt) and adds MakerBridge to **Open with** for .3mf files without changing your default app.
- Engine fixes for Windows that don't change Mac results. See [CHANGELOG.md](CHANGELOG.md).
- **Mac:** nothing changed, so the Mac download is still the 1.1.3 app and shows 1.1.3 in its badge. That's expected.

## What changed in 1.1.3

**Experimental — this update may still have issues. We have not received the original reported 3MF. Generated models were tested, but a complete U1 slice of the new plate/color path is not yet verified. Review all colors, supports and the sliced preview before printing.**

- Projects with more than four palette entries can now be converted **one selected plate at a time** to U1, if the selected plate references at most four filaments.
- Color numbers above four are remapped together with triangle painting and object/part/support assignments. For example, original colors 5 and 8 become toolheads 1 and 2 without changing their assigned colors.
- Missing palette references are rejected in both conversion directions, instead of producing a misleading preservation report.
- The experimental path stops for custom layer-height profiles/layer-range overrides, virtual/mixed filaments, or 3MF material/texture resources. Export the desired plate separately in Bambu Studio for these cases. Object defaults and support assignments count conservatively toward the four-filament limit, even when they might not produce toolpaths.
- The ordinary path for projects with up to four palette entries keeps its existing multi-plate behavior. The reverse direction still supports up to four real filament slots.

See [EXPERIMENTAL.md](EXPERIMENTAL.md) for test coverage and known limits. This is not confirmation that the tester's exact lost-color issue has been fixed.

## First-layer and bed improvements from 1.1.2

See [CHANGELOG.md](CHANGELOG.md) for the release history.

- Added **Use destination printer’s first-layer height**, checked by default, in both conversion directions. With a 0.4 mm nozzle this uses **0.25 mm for U1** or **0.20 mm for Bambu** from the installed printer's default process. Other nozzle sizes use their own native defaults.
- Uncheck it to keep the model's suggested first-layer height, including object/part and layer-range overrides. This choice works independently of **Keep compatible print settings**. If the source has no global first-layer height, the destination default fills that missing value.
- Regular layer height is separate: a 0.12 mm source stays at 0.12 mm when keeping compatible settings. The app now selects the closest ordinary U1 quality preset, including **Fine**, **Optimal** and **Draft** presets in older Snapmaker Orca releases.
- The conversion report records the chosen first-layer mode, height and any removed overrides. The first-layer value is also shown in the conversion notes.
- Custom plate bed-type overrides are cleared in both directions. Every plate follows the slicer's global bed selection, so you can switch from Textured PEI to another supported plate after conversion. Other compatible plate settings remain intact.

## What you need

- **Mac:** Apple silicon (M1 or newer), macOS 13 Ventura or later. Intel Macs aren't supported.
- **Windows:** Windows 10 or 11, 64-bit.
- The destination slicer for the conversion you want to make:

| Conversion | Required slicer |
| --- | --- |
| MakerWorld / Bambu Studio → Snapmaker U1 | [**Snapmaker Orca**](https://www.snapmaker.com/snapmaker-orca), with U1 printer profiles |
| Snapmaker U1 → Bambu / MakerWorld | [**Bambu Studio**](https://bambulab.com/en/download/studio), with your chosen Bambu printer/nozzle profiles |

**Install both slicers only if you want both conversion directions.** The source slicer is not needed just to convert an existing compatible 3MF. On a Mac, install them in **Applications** (your user Applications folder is also supported). On Windows, install them normally; if a slicer lives somewhere unusual (a portable copy, another drive), click **Choose folder…** at the bottom of MakerBridge and pick the folder that contains it. MakerBridge reads native printer, process and material profiles from the installed destination slicer; the slicer does not need to be running during conversion.

Tested with **Snapmaker Orca 2.4.0** and **Bambu Studio 02.08.04.57**. Printer/nozzle choices depend on profiles available in your installed version. Use Snapmaker Orca for U1 exports; Snapmaker Luban and the general OrcaSlicer app are not substitutes for this build's profile lookup.

**Python is included inside MakerBridge. You don't need to install Python or any developer tools.** The slicers are separate downloads and are not included.

## Start

### Windows

1. Run **MakerBridge-Windows-Setup.exe**. Windows SmartScreen will say it "protected your PC" because the installer isn't code-signed yet: click **More info → Run anyway**.
2. Click through the installer. It installs for your user only, so no administrator password is needed.
3. Open **MakerBridge** from the Start menu. You can also right-click a .3mf file and choose **Open with → MakerBridge**.

Using `MakerBridge-Windows-Portable.zip` instead? Extract the whole folder first (right-click → **Extract All**), then run `MakerBridge.exe` inside it. It won't run from inside the zip.

### Mac

Unzip **MakerBridge-Mac.zip** (called `MakerBridge.zip` in releases before 1.1.4), then double-click **MakerBridge.app**. Keep it in this folder or drag it to Applications. The app contains its conversion engine and runtime; the accompanying Licenses folder holds the runtime notices. To share this release, send the complete **MakerBridge.zip**.

This beta is locally signed, but **not Apple Developer ID signed or notarized**. macOS may require you to approve the first launch through System Settings → Privacy & Security → Open Anyway. Only approve a copy you trust.

### MakerWorld → U1

1. Select **MakerWorld → U1**.
2. Click to choose a downloaded MakerWorld print-profile `.3mf` (on a Mac you can also drop it onto the window).
3. Check the colors and nozzle. For projects with more than four palette entries, choose **Plate to convert**; the displayed colors show the selected plate’s new toolhead mapping. Save other plates separately. Projects with up to four palette entries retain their original slots and all plates.
4. Click **Convert & save U1 project** and choose a new filename.
5. Open the result in **Snapmaker Orca**, review the plates, supports, filament assignments and temperatures, then slice and inspect the preview.

### U1 → Bambu / MakerWorld

1. Select **U1 → Bambu / MakerWorld** and choose a Snapmaker U1 project.
2. Choose your **Bambu printer** and matching nozzle size in the app.
3. Click **Convert & save Bambu project** and choose a new filename.
4. Open the result in **Bambu Studio**. Review plate fit, prime-tower placement, materials, AMS routing, color-to-nozzle assignments and supports. Recalculate flushing volumes as appropriate for your setup.
5. Slice, inspect the preview and save the Bambu Studio project before adding it as a MakerWorld print profile.

MakerBridge prepares an editable Bambu Studio project. It does **not** upload to MakerWorld or verify that MakerWorld will accept or approve the profile.

### Bambu printer choices

The picker offers these models when their profiles are present in your installed Bambu Studio:

| Family | Models |
| --- | --- |
| A | A1, A1 mini, A2L |
| P | P1P, P1S, P2S |
| X | X1, X1 Carbon, X1E, X2D |
| H | H2S, H2D, H2D Pro, H2C |

X2D, H2D, H2D Pro and H2C exports retain both physical nozzles, the native nozzle variants and their settings. Bambu Studio assigns colors automatically when slicing. H2C exports also retain the native Vortek hotend configuration; configure your actual hotends and filament routing in Bambu Studio. Source U1 toolhead numbers do not imply an identical physical arrangement on a Bambu printer.

The nozzle selector supports **0.2, 0.4, 0.6 and 0.8 mm** where corresponding installed profiles are available. Both nozzles on dual-nozzle targets use the selected size. The converter selects standard-flow hardware; high-flow or mixed-nozzle setups must be configured and reviewed in the destination slicer.

## Settings and preservation

Leave **Keep compatible print settings** enabled to retain compatible global process settings and selected filament tuning. Turn it off for native destination process/material defaults. The first-layer checkbox is independent of this switch. Object-specific modifiers remain part of the model in either mode, except first-layer-height overrides are removed when using the destination default.

- The ordinary conversion path preserves mesh resources byte-for-byte, including color painting, support painting and seams. Experimental plate selection retains the selected mesh vertices and triangle topology, while rewriting color references to match the new palette; other plates are omitted from that output. Meshes are never scaled or regenerated.
- Object/part structure, modifiers and compatible object overrides are retained. Unsupported options may be removed or replaced and are reported.
- Single- and multi-plate layouts are translated to the destination bed while retaining relative object placement. Ambiguous plate membership fails with a clear error.
- Destination hardware, bed, nozzle, retraction and tool-change settings come from installed native profiles, including Bambu's included G-code templates.
- Filament colors and identities are retained. Bambu nozzle-variant tables are kept separate from color slots, so per-color temperatures do not drift into another slot during a round trip.
- Source machine/filament G-code hooks, sliced G-code, embedded presets and custom per-layer G-code are replaced or removed. Recreate required pauses in the destination slicer. Triangle color painting is retained.
- **Save report…** exports the embedded conversion report, including changed settings, removed files and the source checksum. The report also lives in `Metadata/makerbridge-report.json` inside the output.

Your original is never overwritten. Existing output files are protected too: choose a new filename. Conversion runs on your Mac without uploads, accounts, a local web server or network requests.

## Compatibility and limits

- Ordinary conversion supports **one to four real filament slots**. Experimental MakerWorld → U1 conversion supports larger project palettes by exporting **one plate with at most four referenced filaments**. It never automatically merges colors. Reverse conversion remains limited to four real slots; resolve virtual/mixed slots in the source slicer first.
- Source and target nozzle sizes must match. The app does not redesign extrusion widths for another nozzle diameter.
- Sliced-only `.gcode.3mf`, generic geometry-only 3MF, Cura and PrusaSlicer projects are not supported.
- Textured PEI Plate is selected initially. All plates inherit the global bed selection; change it in the destination slicer to match your actual bed. Review temperatures and material suitability.
- Variable layer profiles are retained in ordinary conversion; experimental plate selection currently refuses them. For U1 exports, enabled Organic/default tree supports become Tree Slim when variable layer profiles or layer-height ranges would cause Orca's unsupported combination. Global and object/part overrides are checked. Other explicit support styles remain unchanged; the report lists adjustments.
- U1 exports use the lowercase standard-flow settings for all four toolheads, fixing the earlier `nozzle_volume_type` warning.
- Bambu prime towers start near the lower-left of each plate, inside the area reachable by every target nozzle. Their final size depends on the slice. Move or rearrange as needed to avoid overlaps; smaller beds may require splitting a plate.
- MakerBridge does not check mesh bounds, prime-tower collisions or toolpath collisions, resize oversized parts, or send jobs to a printer. Destination-slicer review remains necessary.
- Input limit: 512 MB compressed, 1 GB unpacked contents and 20,000 archive entries.
- The bundled app is Apple silicon only. Python 3.13.16 and its required libraries travel with the app; it does not use a system Python installation.

## Validation

**1.1.3:** the rebuilt GUI loaded an eight-color, two-plate generated project, switched to plate 2 and saved its purple/brown regions as toolheads 1/2. Both generated plates passed Bambu Studio slicing after conversion to U1 and back to Bambu. This validates the retained color assignments, not a final U1 toolpath. No original tester file or physical print was tested. The app ZIP is checked after extraction with the bundled Python runtime and no external Python on PATH.

**54 automated checks pass**, including experimental plate selection, shared instances, nested painting, missing color references, support assignments, source protection and variant filament temperatures. Existing checks cover covering source protection, geometry/painting, global and object settings, plate transforms, unsupported inputs, U1 support/nozzle regressions, all 14 Bambu targets, dual-nozzle variant groups, H2C hotends, tower origin, per-color temperature preservation through a round trip, both first-layer modes in both directions, independent print-setting controls, first-layer overrides, nozzle-specific defaults, older U1 quality preset names and per-plate bed inheritance.

**Earlier releases’ bundled runtime passed relocation checks** from a folder containing spaces, with the build-time Python made unavailable and Python search paths disabled. Both conversion directions, H2C/X2D round trips, four colors, geometry preservation and file protection passed. All 48 native binaries link only to bundled libraries or macOS system libraries. The GUI also loaded and saved a four-color U1 conversion using the bundled engine. These checks were performed on the development Mac; a separate clean Mac has not yet been tested.

**Earlier release validation: Bambu Studio 02.08.04.57 successfully sliced four-color sample exports for all 14 Bambu models at 0.4 mm.** All four materials produced toolpaths. X2D/H2D used both extruders; H2C used multiple hotend groups. The A1 mini sample needed its parts repositioned to clear the prime tower. These checks do not establish compatibility with every model, material, nozzle size or future slicer version.

**1.1.2 first-layer validation:** the bundled engine converted both directions with the checkbox on and off, preserving 0.12 mm regular layers and custom support/wall settings. Bambu Studio P1S test slices started at 0.20 mm with destination defaults and 0.25 mm with model settings; subsequent layers remained 0.12 mm. Snapmaker Orca 2.4.0 displayed the 0.12 mm U1 preset with a 0.25 mm first layer and successfully sliced 166 layers. Official Snapmaker Orca 2.3.1 process JSON files also selected the matching 0.12 Fine preset in a regression check; that check used local 2.4.0 machine/material profiles. The tester’s original project was not supplied.

Earlier native GUI validation in **Snapmaker Orca 2.4.0** covered a two-plate sample and the affected helmet plate of `IronManmk46.3mf`. The latter opened without the nozzle-volume substitution notice and sliced with variable layer heights and Tree Slim supports (1,735 layers). The remaining five IronMan plates were not sliced in that check. No physical print or MakerWorld upload was performed.

## How it works

The interface uses SwiftUI/AppKit; the conversion engine is a self-contained helper inside the app. Runtime notices are in `Licenses/` and inside the app. Actual printer, material and process values are loaded from your installed slicers at conversion time.

Format behavior was checked against the official [Snapmaker OrcaSlicer source](https://github.com/Snapmaker/OrcaSlicer) and [Bambu Studio source](https://github.com/bambulab/BambuStudio). Installed slicer profiles remain under their original licenses and are not redistributed. MakerBridge is an independent local utility, not an official Bambu Lab, MakerWorld or Snapmaker product.

## License

Free to download and use; not open source. See [LICENSE](LICENSE). Third-party runtime notices are in `Licenses/`.

Thanks for testing! 

Brian
