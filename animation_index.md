# Animation asset index

This inventory was derived from the uploaded `Split animations.zip` and `Male_spritesheet_all.png`. Names below are exact PNG filename suffixes, not newly assigned action labels. See [animation_rules.md](animation_rules.md) before implementation and [spritesheet_manifest.json](spritesheet_manifest.json) for every measured frame rectangle.

## Verified inventory

- 36 named PNG sheets; 32 distinct decoded sheets; 2,896 occupied cells including duplicate sheets.
- All split sheets are RGBA, 1,280 px wide, with an inferred 128 × 128 px cell grid and 10 columns. 164 fully transparent trailing cells were excluded.
- No internal empty cells were detected. Occupied cells run from index 0 through the last index below.
- The uploaded combined PNG is 79 × 2,048 px. It is an overview; no frame mapping to it has been verified.
- Source timing, loop settings and engine metadata are absent. Cell counts do not establish unique poses or final clip lengths.

## Repository placement

Keep these three files together. To use the supplied paths, extract the original ZIP beside them so the folder is named exactly `Split animations/`; place `Male_spritesheet_all.png` beside them if needed. Images are not included in this documentation package. Alternatively set `asset_base` to your asset directory. Paths use forward slashes and preserve case and spaces.

## Sheets and candidate frame order

For every row, the source is `Split animations/Male_spritesheet_<id>.png`. Read candidate frames left to right, then top to bottom. All indices are zero-based. This is the measured layout, not approval of the full range as one playable action.

| Source ID | Image px | Occupied cells | Candidate indices | Trailing empty cells | Review |
|---|---:|---:|---|---:|---|
| `climb_down_rope` | 1280 × 1024 | 79 | 0–78 | 1 | shared first cell |
| `climb_rope` | 1280 × 1024 | 77 | 0–76 | 3 | boundaries/timing unverified |
| `climb_rope_2` | 1280 × 1024 | 77 | 0–76 | 3 | shared first cell |
| `crouch_idle` | 1280 × 1024 | 74 | 0–73 | 6 | shared first cell |
| `crouch_to_stand` | 1280 × 256 | 20 | 0–19 | 0 | shared first cell |
| `crouch_walk` | 1280 × 640 | 42 | 0–41 | 8 | identical to `crouch_walk_back`; shared first cell |
| `crouch_walk_back` | 1280 × 640 | 42 | 0–41 | 8 | identical to `crouch_walk`; shared first cell |
| `death_1` | 1280 × 1024 | 72 | 0–71 | 8 | identical to `dodge_fwd`; conflicting action labels |
| `death_2` | 1280 × 1408 | 103 | 0–102 | 7 | identical to `dodge_back`; mixed sequence |
| `dodge_back` | 1280 × 1408 | 103 | 0–102 | 7 | identical to `death_2`; mixed sequence |
| `dodge_fwd` | 1280 × 1024 | 72 | 0–71 | 8 | identical to `death_1`; conflicting action labels |
| `dodge_roll` | 1280 × 1024 | 72 | 0–71 | 8 | shared first cell |
| `edge_hang` | 1280 × 1920 | 141 | 0–140 | 9 | shared first cell |
| `falling_idle` | 1280 × 384 | 22 | 0–21 | 8 | shared first cell |
| `falling_landing` | 1280 × 512 | 33 | 0–32 | 7 | shared first cell |
| `find_item` | 1280 × 5376 | 414 | 0–413 | 6 | shared first cell |
| `idle` | 1280 × 768 | 60 | 0–59 | 0 | boundaries/timing unverified |
| `interact` | 1280 × 2432 | 189 | 0–188 | 1 | identical to `push_button`; shared first cell |
| `kick_high` | 1280 × 640 | 41 | 0–40 | 9 | shared first cell |
| `kick_low` | 1280 × 640 | 46 | 0–45 | 4 | shared first cell |
| `kick_spin_high` | 1280 × 768 | 51 | 0–50 | 9 | shared first cell |
| `pull_heavy` | 1280 × 512 | 34 | 0–33 | 6 | shared first cell |
| `pull_lever` | 1280 × 2432 | 189 | 0–188 | 1 | shared first cell |
| `punch_1` | 1280 × 384 | 26 | 0–25 | 4 | shared first cell |
| `punch_2` | 1280 × 384 | 29 | 0–28 | 1 | shared first cell |
| `punch_3` | 1280 × 384 | 27 | 0–26 | 3 | shared first cell |
| `punch_quad` | 1280 × 640 | 47 | 0–46 | 3 | shared first cell |
| `punch_straight` | 1280 × 640 | 45 | 0–44 | 5 | boundaries/timing unverified |
| `push` | 1280 × 3200 | 241 | 0–240 | 9 | shared first cell |
| `push_button` | 1280 × 2432 | 189 | 0–188 | 1 | identical to `interact`; shared first cell |
| `rope_hang` | 1280 × 896 | 65 | 0–64 | 5 | shared first cell |
| `run` | 1280 × 256 | 18 | 0–17 | 2 | shared first cell |
| `run_back` | 1280 × 256 | 20 | 0–19 | 0 | shared first cell |
| `run_jump` | 1280 × 384 | 27 | 0–26 | 3 | boundaries/timing unverified |
| `wall_hang` | 1280 × 896 | 70 | 0–69 | 0 | shared first cell |
| `wall_jump` | 1280 × 512 | 39 | 0–38 | 1 | shared first cell |

## Source anomalies to review

Identical decoded sheets have different filenames:

- `crouch_walk` = `crouch_walk_back`
- `death_1` = `dodge_fwd`
- `death_2` = `dodge_back`
- `interact` = `push_button`

Visual samples of `death_1` / `dodge_fwd` show a fall ending in a lying pose. `death_2` / `dodge_back` include a fall/lying sequence followed by upright movement. Preserve the source labels and review the complete sheets before deciding which action to implement.

The following exact pixel matches suggest shared export boundaries. They do not prove that cell 0 should be removed:

| Sheet cell 0 | Matches final occupied cell of |
|---|---|
| `climb_down_rope` | `climb_rope` |
| `climb_rope_2` | `climb_down_rope` |
| `crouch_idle` | `climb_rope_2` |
| `crouch_to_stand` | `crouch_idle` |
| `crouch_walk` | `punch_straight` |
| `crouch_walk_back` | `punch_straight` |
| `dodge_roll` | `death_1`, `dodge_fwd` |
| `edge_hang` | `rope_hang` |
| `falling_idle` | `dodge_roll` |
| `falling_landing` | `falling_idle` |
| `find_item` | `falling_landing` |
| `interact` | `push` |
| `kick_high` | `kick_low` |
| `kick_low` | `wall_jump` |
| `kick_spin_high` | `kick_high` |
| `pull_heavy` | `kick_spin_high` |
| `pull_lever` | `pull_heavy` |
| `punch_1` | `interact`, `pull_lever`, `push_button` |
| `punch_2` | `punch_1` |
| `punch_3` | `crouch_walk`, `crouch_walk_back` |
| `punch_quad` | `punch_3` |
| `push` | `punch_2` |
| `push_button` | `push` |
| `rope_hang` | `find_item` |
| `run` | `run_back` |
| `run_back` | `interact`, `pull_lever`, `push_button` |
| `wall_hang` | `edge_hang` |
| `wall_jump` | `run_jump` |

No automatic trimming, relabelling or duplicate removal was performed. Repeated poses within an animation may be intentional holds.

## Evidence and limits

Dimensions, occupancy, per-cell alpha bounds, file hashes and full-sheet duplicates were checked programmatically. Representative first, second, quarter, middle, three-quarter and final cells were viewed for all sheets; the complete `run` and `death_2` sheets were also viewed. Semantic boundaries and every intermediate pose have not been individually approved.

The archive contains `Read_me.TXT`, which names a free template pack and links the creator profile. It contains no explicit license terms. This inventory records provenance without assigning a license. The package contains only the three authored reference files.
