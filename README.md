# Latent spectral tables

The colour tables, film data and grain tables behind the **Spectral** rendering in Latent,
an iPhone camera app that shoots in rolls. They're baked from the film profiles of
[spektrafilm](https://github.com/andreavolpato/spektrafilm), Andrea Volpato's spectral
simulation of analog film. Like those profiles, they're licensed
[CC BY-SA 4.0](SPEKTRAFILM_LICENSE.txt).

```
Derived from spektrafilm by Andrea Volpato
https://github.com/andreavolpato/spektrafilm
Licensed CC BY-SA 4.0
Modified by relaxer12 (Latent); the changes are in CHANGELOG.txt.
```

## What's here

One set per Latent stock, named after the stock's id, in `tables/`:

| Latent stock | Film | Printed on |
|---|---|---|
| `portrait160`, `portrait400`, `portrait800` | Kodak Portra 160, 400, 800 | Kodak Portra Endura |
| `ekstar100` | Kodak Ektar 100 | Kodak Portra Endura |
| `golden200` | Kodak Gold 200 | Kodak Portra Endura |
| `ultra400` | Kodak UltraMax 400 | Kodak Portra Endura |
| `pro400h` | Fujifilm Pro 400H | Fujifilm Crystal Archive Type II |
| `ectochrome100` | Kodak Ektachrome 100 | (slide, scanned) |
| `velvet50` | Fujifilm Velvia 100 | (slide, scanned) |
| `cinema800t` | Kodak Vision3 500T | Kodak Vision 2383 |
| `cinema400d` | Kodak Vision3 250D | Kodak Vision 2383 |

Latent's Midnight 500T and Daybreak 250D use the `cinema800t` and `cinema400d` files.

- **`<id>-spectral.bin`**: seven 33³ colour tables, one for each whole stop of exposure
  error from −4 to +2, sRGB code in (red slowest, blue fastest) and sRGB code out, as
  little-endian UInt16 over 0…65535.
- **`<id>-spectral.json`**: the film's data for what happens across the picture:
  - `exposure`: log10 film exposure for each 8-bit code along the grey axis
  - `silver`: each layer's silver density over `silverFrom`…`silverTo` (log10 exposure); on a slide, the silver that hasn't turned to dye
  - `couplers`: the DIR coupler matrix (donor layer row, receiver layer column, log10 exposure per unit density)
  - `couplerUm`, `couplerTailUm`, `couplerTailWeight`: how far the inhibitors spread
  - `scatterUm`, `scatterWeight`: light scattered in the emulsion
  - `grainUm`, `grainN`: the grain tables' pixel size and grid
- **`<id>-spectral-grain.bin`**: for a 9³ grid of codes and each of the seven stops, a 3×3
  taking one unit of each dye layer's grain noise to each output colour, for a pixel
  `grainUm` µm across on the film, as little-endian Float32.

How they were made, and how they differ from spektrafilm's own rendering, is in
[CHANGELOG.txt](CHANGELOG.txt). No spektrafilm code is included here or in the app; it was
only run, offline, to bake these files.

## Licence

CC BY-SA 4.0, as in [SPEKTRAFILM_LICENSE.txt](SPEKTRAFILM_LICENSE.txt), the spektrafilm
licence file, kept unchanged as it asks. Any copy or derivative must credit Andrea Volpato
and https://github.com/andreavolpato/spektrafilm, carry the licence, say that it has
been modified and by whom, and stay CC BY-SA 4.0.
