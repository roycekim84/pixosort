# PixoSort UI Mockup Reference

This document records the current visual direction for the PixoSort UI mockup.

The uploaded concept board should be used as a visual reference while implementing the Flutter UI.

## Reference Board Summary

The board contains these main screens:

1. Home / Stage Select Screen
2. Puzzle Play Screen
3. Clear Result Popup
4. Collection Screen

It also contains these supporting overlays:

A. Pause Popup
B. Settings Bottom Sheet
C. Image Detail Popup
D. Photo Puzzle Creation Sheet
E. Next Stage Confirmation Popup

## Important UI Direction From The Mockup

- Use a warm cream background.
- Use rounded panels and soft shadows.
- Keep pixel art crisp and readable.
- Use a cute but clean pixel-art style.
- Keep the game in portrait orientation.
- Home, difficulty, and stage selection should stay combined in one screen.
- PuzzleScreen should clearly show:
  - framed pixel image
  - bottom-center drain hole
  - active tube under the hole
  - tube row or carousel
  - progress and rotation count
- Clear result should be a popup, not a full page.
- Settings should be a bottom sheet, not a full page.

## Screen Notes

### Home / Stage Select

The mockup shows:

- PixoSort logo
- cute pixel cat preview
- difficulty cards
- 10 stage cards
- photo puzzle button
- collection button

Implementation should follow this compact structure.

### Puzzle Play

The mockup shows:

- top controls
- rotation count
- progress
- framed pixel image
- one drain stream from the hole
- active tube in the center
- color tubes below
- next color preview

Implementation should preserve the one-hole drain identity.

### Clear Result Popup

The mockup shows:

- darkened gameplay background
- centered clear card
- completed pixel image
- stars
- rotation count
- accuracy
- buttons for home, next stage, collection

### Collection

The mockup shows:

- filter tabs
- completed image cards
- locked silhouettes
- clear count

### Supporting Overlays

Use overlays for pause, settings, image detail, photo puzzle options, and next-stage confirmation.

## File Note

The original visual mockup image was generated in chat and should be saved into the repository as an image asset when editing from a local workstation.

Recommended path:

```txt
docs/design/pixosort_ui_mockup_board.jpg
```

After saving the image, embed it here with:

```md
![PixoSort UI Mockup Board](pixosort_ui_mockup_board.jpg)
```
