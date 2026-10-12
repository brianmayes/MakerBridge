# MakerBridge changelog

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
- Added a visible Beta label, developer credit for **Brian Mayes**, and a feedback link to **brian_mayes@me.com**.
- Documented slicer requirements by conversion direction, setup steps and first-launch approval for this locally signed, non-notarized beta.
- Included runtime license notices and verified the bundled engine after relocation with Python search paths disabled.

## 1.1.0 — October 10, 2026

- Added U1 → Bambu/MakerWorld conversion and an in-app Bambu printer/nozzle selector, covering 14 installed printer profiles including P2S, X2D, H2D and H2C.
- Added visible app version information and handling for dual-nozzle and H2C hotend profiles.
- Validated four-color sample exports by slicing for all 14 Bambu targets at 0.4 mm. No physical print or MakerWorld upload was performed.

Developed by Brian Mayes. Feedback: [brian_mayes@me.com](mailto:brian_mayes@me.com).
