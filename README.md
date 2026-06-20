# Trig Level — Precision Check

A small PWA for cross-checking trigonometric leveling measurements between
multiple survey stations in the field.

You pick one station as the reference, enter its zenith angle and instrument
height to the target, and the app shows the **expected zenith angle range** for
every other station. If your next station reads outside the range, something
is off — saving you a long walk back to re-measure later.

## Features

- Editable list of stations (coordinates, elevation, default instrument height)
- Editable target coordinates and base elevation
- Configurable height tolerance for the predicted range (default ±0.5 m)
- Curvature + refraction correction toggle (matters at km-scale sights)
- Works offline once loaded
- Installable to home screen on iOS and Android

## Hosting on GitHub Pages

1. Create a new public repo, e.g. `trig-level`.
2. Copy all the files in this folder into the repo root:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icons/icon-192.png`
   - `icons/icon-512.png`
3. Commit and push.
4. In the repo settings → **Pages**, set the source to `main` branch, `/ (root)`.
5. Wait a minute. Your app will be live at
   `https://<your-username>.github.io/<repo-name>/`.

## Install on your phone

- **iOS (Safari):** open the URL, tap the share button, then *Add to Home Screen*.
- **Android (Chrome):** open the URL, tap the three-dot menu, then *Install app*
  (or *Add to Home screen*).

After installing, the app runs offline.

## Math

For a zenith angle *z* measured from the vertical (so 90° is horizontal),
horizontal distance *H* between station and target:

```
vertical rise  V = H / tan(z)
target elev    = station_elev + instrument_height + V
                  (+ 0.0675 · D_km²  if curvature+refraction is on)
```

The "expected zenith" for a non-reference station inverts the same equation
using the target elevation computed from the reference. The "range" is what
zenith angles would correspond to target elevations ± your chosen tolerance.

## Notes

- Coordinates use a planar projection — the app assumes you're in the same
  projection system across all stations and the target. If you're mixing
  systems (lat/lon vs UTM, etc.), convert first.
- The curvature+refraction correction uses k ≈ 0.13 (typical daytime). It's
  a useful default but not a substitute for proper reciprocal observations
  on high-precision work.
- Everything is stored in your browser's localStorage; clearing site data
  resets to the built-in defaults.
