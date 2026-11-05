# Animation reference rules for Codex

## Read and locate the source

Before creating, adapting or importing an animation, read `animation_index.md` and `spritesheet_manifest.json`, then inspect the referenced PNG. The index is a measured source inventory. General animation guidance below is authored workflow guidance, not metadata supplied by the creator.

The expected layout is these three files beside an extracted `Split animations/` folder. Manifest `source_path` is resolved against `asset_base`, relative to the manifest. If the original assets are missing, report the missing files and continue only work that does not require their pixels. Do not claim to have visually inspected unavailable images.

## Extract frames without changing alignment

- Preserve exact source IDs and paths. Filename labels are provisional action descriptions; do not silently rename them or infer additional attacks, directions or variants.
- Use the split PNGs. The uploaded combined image is only 79 × 2,048 px and has no verified cell mapping.
- Use 128 × 128 px cells, 10 columns, zero offset and zero spacing. Coordinates start at the top left. Indices are zero-based.
- For candidate index `i`, `x = (i % 10) * 128`, `y = floor(i / 10) * 128`; crop `[x, y, 128, 128]`. Use only indices listed in `frames`; trailing transparent cells are padding.
- Keep the entire cell canvas and transparency. `alpha_bounds_in_cell` describes visible content; it is not a replacement crop or pivot. Independent tight crops will lose alignment unless offsets are retained.
- Preserve source pixels for reference/import. Use nearest-neighbor display scaling for pixel inspection. Choose an export resolution deliberately for new art; do not infer one from the tiny overview image.

## Review sequences before making playable clips

The manifest lists occupied cells in geometric row-major order. It does not certify that a whole sheet is one correctly named clip. Review the complete sequence, especially the first cell, row wraps and last cell. Inspect abrupt pose changes and all flagged duplicate or mixed sequences.

Four sheet pairs are pixel-identical despite different labels. Consult `identical_sheet_ids`; do not treat those labels as evidence of distinct motions. `first_cell_matches_last_cell_of` records exact shared boundary cells. These may reflect export overlap, but do not remove them automatically. Save any approved trimming or relabelling as a separate, explicit decision with the source ID and inclusive index range.

Do not deduplicate repeated poses within clips automatically: they may encode holds. Do not reverse `run` to manufacture `run_back`, or assume a back-labelled file depicts opposite facing. Preview the supplied pixels and establish intended motion first.

FPS, frame durations, looping, root motion, origins, collision masks and gameplay events are unknown (`null`). Null means unspecified, not zero or false. Do not replace these with guessed source facts. A playback preview may use a clearly labelled temporary speed; its setting must not become source metadata. Confirm final playback timing and loop seams through visual review and game context.

## Use the reference for new animation

- Maintain the target character's proportions, costume, palette, camera angle and lighting across poses. The reference uses contrasting body-part colors; those colors do not establish a required final costume or rig.
- Study pose progression, balance, arcs and weight shifts. Add anticipation, contact and recovery deliberately when the intended action requires them; do not label exact source event frames without review.
- Keep a stable canvas and chosen anchor. Check foot contacts and held-object contacts for unintended sliding. Decide how actual game movement relates to the animation before implementing motion.
- Establish a shared origin for compatible states through project-specific review; the source includes no declared pivot. For jumps, hangs and falls, verify alignment with the game's world and collision rules.
- Define collisions separately from visible alpha bounds. Draw attacks do not establish hitboxes, damage frames, invulnerability or combo windows. Those require gameplay decisions.
- Treat looping idles/movement and one-shot actions as design choices pending review. Validate transitions in the game and do not assume arbitrary frame counts or speed settings from the filenames.

## Import and verification

For an engine such as GameMaker, import or assemble frames in the manifest order with each frame on the full 128 × 128 canvas. Ensure the importer excludes trailing empty cells and preserves the chosen origin; do not assume the entire PNG is a single horizontal strip. Set animation speed and collision behavior explicitly after review.

Before committing derived assets:

1. Check file hashes against the manifest, or regenerate measurements if source files changed.
2. Verify every selected rectangle is in bounds and the extracted sequence has the intended number and order of frames.
3. Preview the complete sequence against a contrasting background, including row wraps, first/last transitions and the loop seam if looping is chosen.
4. Check identity, scale, anchor, transparency and unintended clipping or sliding.
5. Record source IDs, approved ranges, playback settings and any intentional changes. Keep unreviewed fields unresolved.
6. Report remaining uncertainties and the checks actually completed. Do not describe this inventory as a tested engine integration.

## Repository instructions

To make this workflow discoverable for future Codex tasks, add a reference to these documents in the repository's existing instructions, using their actual repository-relative location. Suggested text:

> Before creating or modifying character animations, read `animation_index.md`, `animation_rules.md` and `spritesheet_manifest.json` at their saved location. Inspect the referenced source images and resolve flagged source anomalies before selecting clip ranges or playback settings.

These three files do not themselves install a permanent memory or automatically change repository instructions. No engine files or repository configuration were modified by this package.
