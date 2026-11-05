# RAW Guru — Community Recipes

The look marketplace for [RAW Guru](https://github.com/electronicturbine/raw-guru). The app reads this
repo directly over HTTPS (`raw.githubusercontent.com`, no account or token needed), so everything here
is plain, reviewable text.

## Layout

- `index.txt` — the catalogue the in-app browser shows. One pipe-separated line per recipe:
  ```
  id | name | author | path/in/repo.rcp | stars
  ```
  `#` comments and blank lines are ignored. `stars` is a cached count maintained in the repo.
- `recipes/*.rcp` — the recipes themselves.

## The `.rcp` format

A tiny line-oriented `key = value` text format (chosen so it diffs and reviews cleanly in pull
requests). Unknown keys are ignored for forward compatibility; `#` starts a comment.

```
name = Morning Haze
author = jane
version = 1
wbGain = 1.04, 0.98          # R, B white-balance gains
colorMatrix = 1,0,0, 0,1,0, 0,0,1
tone = 0,0.06; 0.25,0.28; 1,0.96     # tone curve control points (x,y in 0..1)
hsl = 210:0,0.88,1.0,30; 45:0,1.08,1.03,30   # centreHue:hueShift,sat,lum,width
skinProtect = 0.6            # 0..1, holds skin hues steady under HSL shifts
lut = none                   # or a .cube 3D LUT name
grain = 0.04                 # 0..1
vignette = 0.12              # 0..1
```

Looks are **display-referred** and apply only to the app's JPEG (Tier C) output; RAW / Linear-DNG
captures stay scene-referred so you keep full grading latitude.

## Contributing a recipe

1. Fork this repo.
2. Add your recipe at `recipes/<your-slug>.rcp`.
3. Add a line to `index.txt`:
   ```
   your-slug | Your Look Name | your-name | recipes/your-slug.rcp | 0
   ```
4. Open a pull request. A maintainer reviews it against the naming policy and merges.

### Naming policy

Recipe and author names must be **original**. Do not use protected camera, film-stock, or brand
names (e.g. names that imply an official emulation of another product). Original, descriptive names
only — this keeps the marketplace clear of trademark issues.
