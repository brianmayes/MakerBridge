# Experimental color conversion in 1.1.3

**This beta may still have issues until we can test the original reported 3MF.** The tests used generated cube models, not the tester's commercial file. A successful conversion does not establish that the final U1 toolpath is correct. A complete U1 slice of the new path has not been verified.

## What to try

Open a MakerWorld/Bambu project with more than four palette entries. Choose **Plate to convert**, check the displayed colors, and save a new U1 project. Each output contains only that plate. Repeat for other plates. In Snapmaker Orca, check the colored model, toolhead assignments, supports and every relevant part of the sliced preview before printing.

For example, a project may use red/green on plate 1 and purple/brown from slots 5/8 on plate 2. Selecting plate 2 exports purple/brown as tools 1/2, with the paint references remapped accordingly. Four physical U1 nozzles remain configured. This feature does not add more than four simultaneous physical filaments.

The original file is never overwritten. Keep it for comparison. Older 1.1.2 downloads remain available under Releases if you need to return to that version.

## Known limits

- At most four referenced filaments on the selected plate. Object defaults and support assignments count even when unused by a particular slice; this conservative count may refuse some otherwise printable plates.
- Custom layer-height profiles and layer-range overrides are not supported by this experimental path. Export the desired plate separately in Bambu Studio, reduce unused palette entries there, and use the ordinary conversion path instead.
- Virtual/mixed filament definitions, 3MF material/texture resources, ambiguous plate assignments and broken component/paint references stop conversion with an explanation.
- Existing conversions with four or fewer project slots retain their multi-plate and variable-layer behavior. Reverse conversion still allows up to four real filament slots.
- No physical print or clean second-Mac test has been performed. Matching nozzle size, plate fit, temperatures and collision checks remain necessary in the slicer.

## Checks completed

54 automated tests pass, including source protection, shared component/instance handling, selected-plate transforms, nested paint encoding, color correspondence, support/part references, variant filament temperatures and missing-palette rejection in both directions. The rebuilt GUI successfully selected and saved plate 2 from a synthetic eight-color project.

Both synthetic plates sliced successfully in Bambu Studio after U1 conversion and a reverse conversion to Bambu. Their toolpaths retained the expected red/green and purple/brown materials. These are Bambu slices, not final U1 slices. Prior Snapmaker CLI attempts crashed in its filament-count/plate path; GUI import showed the prototype's correct colors, but a final U1 slice remains unconfirmed.

Paint encoding was checked against the official [Snapmaker TriangleSelector implementation](https://github.com/Snapmaker/OrcaSlicer/blob/main/src/libslic3r/TriangleSelector.cpp) and [Bambu TriangleSelector implementation](https://github.com/bambulab/BambuStudio/blob/master/src/libslic3r/TriangleSelector.cpp). See `Validation.json` for the release record.

## Feedback

Send feedback to **brian_mayes@me.com** with MakerBridge and slicer versions, the selected plate, expected colors and what happened. Screenshots of the original and converted project plus the conversion report are useful. Share a model only if you have permission; a simplified example reproducing the problem is fine. This release is not confirmation that the original reported lost-color issue is fully fixed.
