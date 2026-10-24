# Experimental slicer inputs — MakerBridge

Developed by Brian Mayes. Feedback: hello@printroomhq.com.

Creality Print and Anycubic Slicer Next can supply compatible editable 3MF projects to **3MF → U1** (called **MakerWorld → U1** before 1.1.8). Install Snapmaker Orca for the destination profiles. Bambu Studio remains required for **U1 → Bambu / MakerWorld**; direct conversion from these vendors to Bambu is not offered.

| Input application tested | Source printer/nozzle | Samples |
| --- | --- | --- |
| Creality Print 7.3.0.6157, Mac ARM | Creality K3, 0.4 mm | Basic and variable-layer projects |
| Anycubic Slicer Next 2.0.0.3, Mac ARM | Kobra S1, 0.4 mm | Basic and variable-layer projects |

These four files contain generated cubes, four painted colors and two plates. They are not customer or commercial models. With the **1.1.6 engine**, all 16 archive conversion checks passed: both first-layer modes to U1, then both first-layer modes from U1 to Bambu P1S. Checks covered geometry/painting bytes, color palette, plate membership and relative positions, 0.12 mm regular layers, wall/infill/support settings, object overrides, variable layers and layer-range data, bed inheritance, and original-file protection.

**Bambu Studio 02.08.04.57 sliced all eight plates from the 1.1.6 P1S outputs**, with all four model colors and a 0.20 mm first layer. Skin/skeleton percentage widths now become millimeters using the nozzle diameter. For example, `100%` means `0.4 mm` for a 0.4 mm nozzle, rather than the erroneous 100 mm interpreted from older output. The correction also applies to object/part and layer-range overrides.

**Earlier investigation:** Snapmaker Orca 2.4.0 sliced plate 1 of each vendor's variable-layer U1 sample using the previous Mac 1.1.3 engine: 147 layers, all four filaments and a 0.25 mm first layer. Both had a bed-temperature/filament warning; review material and bed temperatures. These are historical U1 slice results, not new physical print tests. The 1.1.6 fix changes the reverse Bambu direction.

## What this does not establish

- Full compatibility with every Creality/Anycubic printer, future slicer release, older Anycubic Slicer, or arbitrary custom project.
- More than four colors, mixed/virtual filaments, or material/texture resources from these vendors. The existing experimental selected-plate restrictions remain; see `EXPERIMENTAL.md`.
- Windows native-slicer preview testing: vendor-save and native slice checks above were on Mac. Windows builds run conversion regressions, frozen-app and installer checks separately.
- Physical print quality, MakerWorld upload acceptance, or a clean second Mac.

One generated Anycubic shared-instance sample lost its second-plate membership when saved. MakerBridge correctly refused that ambiguous archive. This does not establish that all shared-instance files fail; preserve the original and review any refusal in the source slicer.

Review plates, colors, supports, temperatures and the sliced preview before printing. No print jobs were sent during validation. The original tester's greater-than-four-color project is still unavailable, so that path retains its separate experimental warning.

## Setting definitions

The unit translation follows the official [Anycubic setting definitions](https://github.com/ANYCUBIC-3D/AnycubicSlicerNext/blob/master/src/libslic3r/PrintConfig.cpp) and [Bambu setting definitions](https://github.com/bambulab/BambuStudio/blob/master/src/libslic3r/PrintConfig.cpp).
