# Love Heart

An animated heart built entirely from "I love you" written in 20 languages, drawn with Python's `turtle` and `tkinter`. The phrases rise into place one by one in a purple gradient, then the finished heart shimmers continuously.

<p align="center">
  <img width="48%" alt="Love Heart screenshot 1" src="https://github.com/user-attachments/assets/f4168d6c-f655-4cbe-9474-e3f165abaf32" />
  <img width="48%" alt="Love Heart screenshot 2" src="https://github.com/user-attachments/assets/1abea926-d6ef-4f36-8b43-a90b767ffce1" />
</p>

## Features

- Heart outline from a parametric curve, filled row by row with text
- 20 languages: English, Turkish, Spanish, French, German, Italian, Portuguese, Russian, Korean, Japanese, Chinese, Hindi, Greek, Dutch, Swedish, Polish, Thai, Vietnamese, Indonesian, Ukrainian
- Phrases are fitted and spaced to each row so edges line up with the heart's shape
- Purple colour gradient (deep purple at the centre to light violet at the edges)
- Phrases fade in, drift up into position and flash briefly as they land
- Edge phrases appear first (tracing the outline), then the inside fills in
- After the animation, random phrases shimmer forever

## Requirements

- Python 3.8+
- `tkinter` (bundled with most Python installs; on Debian/Ubuntu: `sudo apt install python3-tk`)
- A font with the needed scripts. Default is `Arial`; if some characters (Hindi, Thai, Korean, etc.) show as boxes, change `FONT` to a font that covers them, e.g. `Noto Sans`.

No third-party packages are needed.

## Run

```bash
python heart.py
```

Replace `heart.py` with whatever you named the script. An 800x800 window opens and the animation starts automatically. Close the window to quit.

## Configuration

Edit the constants at the top of the file:

| Constant | Default | Meaning |
|----------|---------|---------|
| `SC` | `21` | Heart scale (bigger = larger heart) |
| `OY` | `20` | Vertical offset of the heart |
| `DURATION` | `10` | Seconds to spawn all phrases |
| `TICK` | `16` | Milliseconds per animation frame |
| `ANIM` | `42` | Frames each phrase takes to settle |
| `LIFT` | `34` | Pixels a phrase rises from when it appears |
| `GAP` | `7` | Horizontal spacing between phrases |
| `SIZES` | `(9, 10, 11, 12)` | Font sizes picked at random |
| `FONT` | `"Arial"` | Font family |
| `BG` | `"#070208"` | Background colour |

To change the colours, edit `wine`, `crimson` and `blood` inside `build()`. To change the glow of the landing flash and shimmer, edit `FLASH`.

To add or remove languages, edit the `PHRASES` list.

## How it works

1. `heart()` samples a parametric heart curve into a polygon.
2. `spans()` and `intersect()` find the horizontal slice of the heart available at each text row.
3. `build()` packs random phrases into each slice, spreads them to fill the width, colours them by distance from the centre, and orders them (outline first, then inside).
4. `step()` spawns phrases at a steady rate; `animate()` handles each phrase's fade, rise and flash, using a shadow and halo text item for depth.
5. When all phrases have landed, `shimmer()` keeps lighting random phrases.

The random seed is fixed (`Random(11)`), so the layout is the same on every run. Change the seed for a different arrangement.
