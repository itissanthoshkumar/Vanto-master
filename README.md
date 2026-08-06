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
- **14th-floor context** — the flat sits at its real height above a
  reconstruction of the 12.5-acre site (3 towers, clubhouse, pool, courts,
  amphitheatre, cycling loop).

## Accuracy

Room dimensions, wall positions, door openings and sanitary fixtures are taken
from the GFC drawings (architectural, electrical, plumbing) by extracting the
PDF vector geometry — all 11 rooms match their printed dimensions to ≤25 mm.

**The site/amenity layout is a reconstruction.** Trifecta publishes the amenity
list but not a dimensioned master plan, so the grounds are indicative.

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
