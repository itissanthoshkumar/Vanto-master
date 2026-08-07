# B-1428 & 1429 · Trifecta Vanto — Interactive 3D Walkthrough

An interactive 3D walkthrough of flat **B-1428 & 1429, Tower B, Trifecta Vanto**
(Kodathi Village, Sarjapur Road, Bengaluru) — two 1BHKs combined into a single
1425 sqft 3BHK.

Everything is a single self-contained `index.html`: Three.js from a CDN, all
geometry generated procedurally, no build step and no asset files.

## Run it

```bash
python3 run_preview.py     # serves on http://127.0.0.1:8791
```

Or just open `index.html` directly in a browser.

> **macOS note:** apps spawned by some tools can't read `~/Documents`. If the
> server fails to start, copy `index.html` + `run_preview.py` to `/tmp/` and run
> it from there.

## What's in it

- **Autoplay walkthrough** — starts on its own, ~2:13, 59 stops with captions.
  Player bar has pause, stop-skip, a scrubbable progress track, speed
  (1× / 1.5× / 2× / 3×), **Save video** (records to `.webm`) and **Explore ✕**.
  Add `?noauto` to the URL to suppress autoplay.
- **Free walk** — WASD + pointer lock, with a drag-to-look fallback and touch
  controls (left half moves, right half looks).
- **Overview** — orbitable dollhouse; click any room on the floor map to jump
  there, or double-click the model to drop in.
- **Toggles** — Labels · Amenities · Realistic · Roof · Evening · Ghost walls ·
  Pigeon net · 2×1BHK · Reset.
- **14th-floor context** — the flat sits at its real height above the
  12.5-acre site, laid out from the project's landscape master plan: three
  towers, the 50,000 sqft clubhouse, the water body, pool, amphitheatre,
  courts, Miyawaki forest and the 2.5 m cycling loop. Amenity pins carry the
  master plan's own numbering.

## Accuracy

Room dimensions, wall positions, door openings and sanitary fixtures are taken
from the GFC drawings (architectural, electrical, plumbing) by extracting the
PDF vector geometry — all 11 rooms match their printed dimensions to ≤25 mm.

The site follows the project's landscape master plan (the eagle-view drawing
with the 74 numbered amenities). Our flat is the **west-face unit at the north
end of Tower B**, so the balcony looks west over the tennis court, the water
body, the fountain and the clubhouse, and north over the football ground.
Compass in model space: `-x` west, `+x` east, `-z` north, `+z` south.

Furniture is laid out to the same dimensions, and where the room is tight the
layout says so rather than pretending otherwise. The living room is only 3.20 m
from the door wall to the media wall, and the sofa's back cannot come north of
z 4.32 without closing the walking lane to the bedroom / toilet / study doors —
so the depth left in front is 2.19 m. The seating is an L-sectional wrapping the
north-east, the TV sits in a full-height unit (white lacquer carcass, backlit
walnut open shelves, continuous base run on a recessed plinth), and the set is
sized to the ~1.5 m throw the room allows — 55", not 65".

The master plan is not dimensioned, so amenity positions are scaled off the
drawing (≈0.21 m per drawing pixel, which lands the site at 12.4 acres against
the published 12.5) — the arrangement is right, the metre-level positions are
close rather than surveyed.

## Built-in QA

Open the console and call:

| Hook | Checks |
|---|---|
| `__qaLanes()` | every doorway has a clear walking lane |
| `__qaLegs()` | no tour leg crosses a wall |
| `__qaPoints()` | no viewpoint sits inside furniture |
| `__qaAlign()` | furniture that should be flush to a wall but isn't |
| `__qaViews()` | viewpoints facing a wall too closely |
| `__qaWhat(x,z)` | names the colliders at a point |
| `__qaWalk(key, secs)` | steps the real movement code deterministically |

Also `__walkTo(x, z, yawDeg)`, `__orbitTo(θ, φ, r)`, `__pos()`.
