# MakerBridge changelog

## 1.2.2 Beta — October 24, 2026

- **Variable layer heights in plate selection.** Converting one plate of a project that uses more than four colors now keeps the custom layer-height profiles, height-range modifiers, brim ears and cut info of that plate's objects. Before, these projects stopped with "Experimental plate selection does not yet support custom layer-height profiles or layer-range overrides", and Combine colors couldn't be used on them.
- Bambu Studio and Orca number these per-object entries by each object's place in the build list, not by its ID. MakerBridge keeps only the selected plate's entries and renumbers them for the new file. A height range's filament follows the plate's new toolhead numbering and counts as one of the plate's colors, so it shows up in Combine colors.
- A per-object file MakerBridge can't read stops the conversion with an explanation; nothing is guessed.
- The update check now sends the app version, Mac or Windows, and a random ID the app makes on first launch, so printroomhq.com can count active copies by version. Nothing about the user, their computer or their files is sent.
- Tested on a two-plate H2D project built from a tester's six-color helmet plus a test block, with a variable layer-height profile and a height-range color change. The block was object 2 in the source and object 1 in the output. Reverse-converted to a P1S, its plate sliced in Bambu Studio with 415 layers instead of 200 without the profile, and the range's color printed from exactly 20 to 30 mm. The helmet plate converted with green and gray combined into black, and its height range was kept. The Snapmaker Orca command-line slicer still crashes on this Mac, so check the U1 preview in the app.
- Validation: 81 automated tests passed on Mac (5 new for per-object layer files, 1 for the update check).

## 1.2.1 Beta — October 23, 2026

- **Combine colors.** A plate that uses more than four colors no longer stops with an error. MakerBridge shows each color with roughly how much of the printed surface it covers, and suggests which colors to print with another color's toolhead: the least-used color goes to the closest remaining color, repeated until four are left. Each choice is a dropdown on Mac and Windows; **Use suggestion** puts the defaults back. Convert stays off until the plate fits four toolheads.
- Combined colors keep their painting. Their painted faces, object and part assignments and support settings move to the kept color's toolhead together, and the conversion report and review notes list every merge with its surface share. A material mismatch (for example PETG printed as PLA) is called out.
- One-plate projects no longer show the plate picker.
- Command line: `--combine 3:2,5:2` prints source colors 3 and 5 with color 2's toolhead (3MF → U1 only).
- Tested on a tester-supplied six-color H2D project: green (0.8% of the surface) and gray (under 0.1%) were combined into black, giving a four-color U1 project. Reverse-converted to a P1S, it sliced in Bambu Studio with all four colors (673 layers). The Snapmaker Orca command-line slicer still crashes on this Mac, so check the U1 preview in the app. The model itself is not bundled or published.
- Validation: 76 automated tests passed on Mac (5 new for combining colors).

## 1.2.0 Beta — October 21, 2026

- **Updates inside the app.** MakerBridge checks printroomhq.com for a new version when it opens (and from **Check for updates** at the bottom of the window, or MakerBridge › Check for Updates… on Mac). When one is out, a bar offers **Update**: Mac swaps the app in place and reopens it; Windows downloads the installer, reinstalls quietly for the current user and reopens. Portable Windows copies get a link to the download page instead.
- Every update is checked before it's used: the version information must carry the publisher's Ed25519 signature, and the downloaded file must match the signed size and SHA-256. Anything else is ignored.
- Feedback now goes to hello@printroomhq.com.
- Conversion is unchanged from 1.1.8.

## 1.1.8 Beta — October 14, 2026

- Clarified supported input slicers inside both Mac and Windows apps. The forward tab is now **3MF → U1**, with a persistent **Compatible inputs** card listing MakerWorld / Bambu Studio and experimental Creality Print / Anycubic Slicer Next.
- Updated the subtitle, drop area, file chooser and error guidance for editable project 3MFs. Older Anycubic Slicer is explicitly excluded.
- Conversion behavior, including 1.1.7 all-plate preservation, remains unchanged. This is a wording/interface update, not a broader compatibility claim.
- Validation: 66 automated checks passed on each platform, packaged conversion checks passed, and the new card was visually checked in empty and loaded states on Mac and Windows. Windows installation and file-drop checks passed.

## 1.1.7 Beta — October 14, 2026

- Fixed unused saved filament slots forcing a multi-plate Bambu project into single-plate export. When the whole project references at most four real filaments, preserve every plate and compact only unused slots. Keep painting, object/part/support/range references and matching filament tuning together; do not merge colors.
- Preserve custom layer profiles and range overrides in this all-plate path. Keep the existing experimental single-plate behavior when more than four filaments are actually referenced, including its existing unsupported-input limits.
- Preserve volume-local assembly transforms while translating plate-level instances to the destination bed layout.
- Added five synthetic regression tests; all 66 automated tests passed on Mac. Reproduced the five-plate/three-used-slot case using a locally supplied project. Personal models are not bundled or uploaded. See Validation.json and the release notes for packaged-build checks.

## 1.1.6 Beta — October 13, 2026

- Updated **both Mac and Windows** to the same conversion engine and version. Bundled Python/runtime, existing installer behavior and Windows drag and drop remain included.
- Fixed percentage-based `skin_infill_line_width` and `skeleton_infill_line_width` being read as enormous millimeter widths by Bambu Studio. Translate using the matching nozzle diameter (`100%` → `0.4 mm` on a 0.4 mm nozzle) in project settings, object/part metadata and layer-range overrides. Preserve existing absolute widths and record translations in the conversion report.
- Refuse malformed/non-finite/negative values in retained width settings before creating an output. Native process mode keeps destination global widths and still translates retained object/range overrides.
- First-layer default/model choices, regular layer heights, plate-bed inheritance and color handling are unchanged.
- Documented **experimental Creality Print and Anycubic Slicer Next inputs**, using MakerWorld → U1. No direct Creality/Anycubic destination or direct-to-Bambu mode was added. Older Anycubic Slicer variants are not covered.
- Mac validation: 61 automated tests, 16 archive checks on four vendor-saved generated projects, and successful native Bambu slices of all eight converted plates. Windows builds run the same suite plus frozen-engine, installation and file-drop checks; see the completed results in the release notes. No physical print or broad printer compatibility claim. Details: `COMPATIBILITY.md`.

## 1.1.5 Beta — October 2026

- **Windows: drag and drop.** Drop a .3mf from File Explorer anywhere on the window to load it. It also works if MakerBridge was started as administrator. Dropping something other than a .3mf shows a message instead of loading it.
- Windows license notes use US spelling.
- Mac: unchanged. The Mac download is still the 1.1.3 app.
- Validation: the automated Windows build sends the installed app the same message a File Explorer drop produces, and checks that it loads the dropped project. A drag with the mouse on a real PC hasn't been tried yet.

## 1.1.4 Beta — October 2026

**MakerBridge for Windows.** Same converter and the same options as the Mac app, in both directions.

- New Windows app (Windows 10/11, 64-bit): installer (`MakerBridge-Windows-Setup.exe`, per-user, no administrator prompt) or portable `MakerBridge-Windows-Portable.zip`. Adds MakerBridge to **Open with** for .3mf files without changing your default app.
- Finds Snapmaker Orca and Bambu Studio where their Windows installers put them. If a slicer lives somewhere else, **Choose folder…** remembers its location.
- Engine fixes that matter on Windows and do not change Mac results: slicer profiles are read as UTF-8, paths inside the 3MF are always handled as forward-slash archive paths, and the converted file can be saved to drives without hard links (exFAT/FAT USB drives, some network shares) — still never replacing an existing file.
- Mac: nothing changes in this release, so the Mac download stays MakerBridge 1.1.3. Conversions are identical with either engine.
- Validation on GitHub's Windows Server 2022 machines with Snapmaker Orca 2.4.0 and Bambu Studio 02.08.04.57 installed by their own installers: both slicers found automatically, 54 automated checks pass, and the installed app converted a non-ASCII-named project to U1 and back to Bambu A1 and X2D. Not yet tried on a tester's Windows PC; no physical print.
## 1.1.3 Beta — October 11, 2026

**Experimental color update: may still have issues until the original reported 3MF can be tested. A complete U1 slice of the new path is not verified.**

- Added a plate picker for MakerWorld projects with more than four palette entries. Each output contains one selected plate with at most four referenced filaments; convert other plates separately.
- Remaps color painting and object/part/support references together with their palette. Shared components and repeated instances are retained for the selected plate, with its layout translated onto the U1 bed.
- Detects missing palette references in both directions before writing an output. Stops instead of silently discarding or merging colors.
- Experimental selection currently refuses custom layer-height data/range overrides, virtual/mixed definitions and 3MF material/texture resources. Defaults and support references count conservatively toward the four-color limit.
- Existing first-layer defaults, bed inheritance and reverse printer choices remain available. Python and the conversion engine are still bundled.
- Validation: 54 automated checks pass; rebuilt GUI loaded and saved plate 2 of a generated eight-color project. Both generated plates sliced in Bambu Studio after U1/Bambu conversion. No tester model or physical print was tested; final U1 slicing remains unverified. See EXPERIMENTAL.md and Validation.json.

## 1.1.2 Beta — October 11, 2026

- Added **Use destination printer’s first-layer height**, checked by default, for both MakerWorld/Bambu → U1 and U1 → Bambu/MakerWorld conversions.
- With the checkbox checked, use the installed destination printer's default process to choose the first-layer height: **0.25 mm for U1** and **0.20 mm for Bambu** with a 0.4 mm nozzle. Other nozzle sizes use their own native defaults. Remove conflicting first-layer-height overrides at object, part and layer-range levels.
- Uncheck it to preserve the source model's suggested first-layer height and overrides. This option is independent of **Keep compatible print settings**. A missing source value falls back to the destination default.
- Keep regular layer height separate from first-layer height. A custom 0.12 mm project retains its 0.12 mm regular layers when keeping compatible settings.
- Fixed U1 preset selection in older Snapmaker Orca releases: consider ordinary **Fine**, **Optimal**, **Draft** and **High Quality** presets as well as **Standard**, and select the closest available layer height. Specialized color-mixing and support-material presets are excluded from automatic selection.
- Record the selected first-layer mode, value, destination default profile and removed overrides in the conversion report. Show the chosen global first-layer value in the conversion notes.
- Fixed custom plate bed types getting stuck on Textured PEI after conversion. Converted plates now inherit the slicer's global bed selection in both directions, so changing the selected bed type updates them. Other compatible plate settings are retained; removed bed-type overrides are listed in the report.
- Added regression coverage for both modes and conversion directions, object/part/range overrides, missing source values, nozzle-specific defaults, renamed/older presets and per-plate bed inheritance. **42 automated checks pass.**

## 1.1.1 Beta — October 10, 2026

- Bundled Python 3.13.16 and required runtime libraries inside the Mac app. Testers no longer need to install Python, Xcode or developer tools.
- Added a visible Beta label, developer credit for **Brian Mayes**, and a feedback link (now hello@printroomhq.com).
- Documented slicer requirements by conversion direction, setup steps and first-launch approval for this locally signed, non-notarized beta.
- Included runtime license notices and verified the bundled engine after relocation with Python search paths disabled.

## 1.1.0 — October 10, 2026

- Added U1 → Bambu/MakerWorld conversion and an in-app Bambu printer/nozzle selector, covering 14 installed printer profiles including P2S, X2D, H2D and H2C.
- Added visible app version information and handling for dual-nozzle and H2C hotend profiles.
- Validated four-color sample exports by slicing for all 14 Bambu targets at 0.4 mm. No physical print or MakerWorld upload was performed.

Developed by Brian Mayes. Feedback: [hello@printroomhq.com](mailto:hello@printroomhq.com).
