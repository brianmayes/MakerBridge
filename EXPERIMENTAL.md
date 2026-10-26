# Multi-plate color handling and experimental plate selection

**This beta may still have issues until we can test the original reported 3MF.** The tests used generated cube models, not the tester's commercial file. A successful conversion does not establish that the final U1 toolpath is correct. A complete U1 slice of the new path has not been verified.

## All-plate conversion in 1.1.7

A palette may contain unused material slots. MakerBridge now checks references across the entire archive first. When four or fewer real filaments are referenced, it removes only unused slots and keeps **all plates**. This includes references in painted faces, object/part settings, supports and layer-range overrides. Custom layer profiles remain intact because object and instance numbering does not change. The conversion report lists the original slots and their U1 toolhead mapping.

This path was tested with a locally supplied five-plate project using three of five saved filament slots and with synthetic remapping/range/variant tests. That file is separate from the original greater-than-four-used-color report discussed below. Mixed/virtual definitions and 3MF material/texture resources are not automatically compacted.

## What to try when more than four filaments are actually referenced

Open a MakerWorld/Bambu project that references more than four filaments across its plates. Leave **Plate to convert** on **All plates · one file each** to save every plate as its own U1 project in one step (1.2.3), or choose one plate and check its displayed colors. Each output contains only its plate. In Snapmaker Orca, check the colored model, toolhead assignments, supports and every relevant part of the sliced preview before printing.

For example, a project may use red/green on plate 1 and purple/brown from slots 5/8 on plate 2. Selecting plate 2 exports purple/brown as tools 1/2, with the paint references remapped accordingly. Four physical U1 nozzles remain configured. This feature does not add more than four simultaneous physical filaments.

The original file is never overwritten. Keep it for comparison. Older 1.1.2 downloads remain available under Releases if you need to return to that version.

## Combining colors in 1.2.1

U1 has four toolheads. When the selected plate uses more than four colors, MakerBridge no longer stops: it shows each color's approximate share of the printed surface and suggests merges, repeatedly folding the least-used color into the closest remaining one (by a perceptual RGB distance) until four are left. You can change any merge before converting.

A combined color keeps its painting. Every painted face, object or part assignment and support setting that used it is moved to the kept color's toolhead, so it prints in that color. Nothing is deleted from the mesh. The report lists each merge, and a material mismatch is called out. Surface shares are an estimate: painted sub-triangles count equally, and unpainted faces count toward their part's or object's filament.

Tested with synthetic models (paint, support and process references, invalid choices) and a tester-supplied six-color H2D project, where green (0.8%) and gray (under 0.1%) were combined into black.

## Variable layer heights in 1.2.2

Bambu Studio and Orca key per-object layer files (`layer_heights_profile.txt`, `layer_config_ranges.xml`, `brim_ear_points.txt`, `cut_information.xml`) by each object's place in the build list. Plate selection keeps the selected plate's entries and renumbers them. Tested with a two-plate H2D project built from a tester-supplied helmet plus a test block: the block moved from object 2 to object 1, and a P1S reverse conversion of its plate sliced in Bambu Studio with the variable profile (415 layers instead of 200) and the height range's color from 20 to 30 mm.

## Known limits

- At most four toolheads on the selected plate. Above four, colors must be combined (1.2.1). Object defaults and support assignments count even when unused by a particular slice, so they can appear in the combine list with a 0% share.
- Custom layer-height profiles, height-range modifiers, brim ears and cut info are kept for the selected plate's objects (1.2.2). They are renumbered to the objects' new order; a range's filament follows the new toolhead numbering. A per-object file that can't be read stops the conversion.
- Virtual/mixed filament definitions, 3MF material/texture resources, ambiguous plate assignments and broken component/paint references stop conversion with an explanation.
- Existing conversions with four or fewer project slots retain their multi-plate and variable-layer behavior. Reverse conversion still allows up to four real filament slots.
- No physical print or clean second-Mac test has been performed. Matching nozzle size, plate fit, temperatures and collision checks remain necessary in the slicer.

## Checks completed

The original 1.1.3 release passed 54 automated tests, including source protection, shared component/instance handling, selected-plate transforms, nested paint encoding, color correspondence, support/part references, variant filament temperatures and missing-palette rejection in both directions. The rebuilt GUI successfully selected and saved plate 2 from a synthetic eight-color project.

Both synthetic plates sliced successfully in Bambu Studio after U1 conversion and a reverse conversion to Bambu. Their toolpaths retained the expected red/green and purple/brown materials. These are Bambu slices, not final U1 slices. Prior Snapmaker CLI attempts crashed in its filament-count/plate path; GUI import showed the prototype's correct colors, but a final U1 slice remains unconfirmed.

Paint encoding was checked against the official [Snapmaker TriangleSelector implementation](https://github.com/Snapmaker/OrcaSlicer/blob/main/src/libslic3r/TriangleSelector.cpp) and [Bambu TriangleSelector implementation](https://github.com/bambulab/BambuStudio/blob/master/src/libslic3r/TriangleSelector.cpp). See `Validation.json` for the release record.

## Feedback

Send feedback to **hello@printroomhq.com** with MakerBridge and slicer versions, the selected plate, expected colors and what happened. Screenshots of the original and converted project plus the conversion report are useful. Share a model only if you have permission; a simplified example reproducing the problem is fine. This release is not confirmation that the original reported lost-color issue is fully fixed.
