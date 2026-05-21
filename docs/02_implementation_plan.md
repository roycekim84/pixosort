# PixoSort Implementation Plan

## Tech Stack

- Flutter
- Dart
- Local-first architecture
- No required backend for MVP
- Local persistence for progress and settings

The first version should avoid unnecessary dependencies. Keep the puzzle engine testable without Flutter UI.

## Architecture Direction

Use a simple layered structure:

- Presentation: screens, widgets, animations
- Domain: stage models, pixel grid, drain rules, gravity rules, tube models
- Application: game controller, stage loading, photo puzzle generation flow
- Infrastructure: local storage, image processing adapters, ads/IAP adapters

## Core Mechanic Summary

A pixel art image is represented as a 2D grid. The frame has one drain hole at the bottom center. Pixels are pulled toward the hole by grid-based gravity.

If the active tube color matches the pixel currently at the drain hole, that pixel drains into the tube. Draining continues automatically while the hole pixel color remains the same. If the hole pixel color changes, draining pauses until the player activates the matching tube.

## Core Data Models

### StageDefinition

Represents one built-in puzzle stage.

Fields:

- id
- difficulty
- stageNumber
- title
- theme
- width
- height
- palette
- initialPixelMap
- drainHoleX
- drainHoleY
- previewMode
- targetDrainSpeed
- targetRotationCount

### PaletteColor

Fields:

- index
- hex
- name
- symbol optional

### PixelCell

Represents one cell in the pixel grid.

Fields:

- colorIndex nullable
- isEmpty

A null colorIndex means the cell is empty after pixels have drained.

### PixelGrid

A 2D grid of PixelCell values.

Responsibilities:

- Read the color at the drain hole
- Remove the pixel at the drain hole
- Apply gravity after removal
- Count remaining pixels by color
- Determine whether the grid is empty

### DrainHole

Fields:

- x
- y

MVP rule:

- The drain hole is fixed at bottom center.

### ColorTube

Each tube corresponds to one palette color.

Fields:

- colorIndex
- collectedCount
- targetCount
- isComplete

Important rule:

- Color count equals tube count.
- There are no helper tubes in the core mechanic.

### TubeCarousel

Represents the tube selector under the drain hole.

Fields:

- tubes
- activeTubeIndex
- rotationCount

Responsibilities:

- Rotate left
- Rotate right
- Select tube directly if the UI supports tapping
- Return active tube

### DrainState

Fields:

- stageId
- pixelGrid
- tubes
- activeTubeIndex
- drainedPixelCount
- totalPixelCount
- rotationCount
- elapsedTime
- isDraining
- isPausedBecauseColorMismatch
- isCompleted

### DrainResult

Result of one drain tick.

Fields:

- drainedColorIndex nullable
- didDrain
- didCompleteTube
- completedColorIndex nullable
- isBlockedByColorMismatch
- isStageCompleted

### UserProgress

Fields:

- clearedStageIds
- stageStars
- bestRotationCounts
- bestTimes
- unlockedDifficulties
- collectionItems
- settings

## Built-in Stage Data

Built-in stages should be stored as JSON assets.

Suggested path:

```txt
assets/stages/
  level_01.json
  level_02.json
  ...
  level_10.json
```

Each file contains 10 stage definitions.

Stage JSON should store compact pixel maps using palette indexes.

Example:

```json
{
  "id": "level_01_apple",
  "difficulty": 1,
  "stageNumber": 1,
  "title": "Apple",
  "theme": "simple_icon",
  "width": 8,
  "height": 8,
  "palette": ["#000000", "#e74c3c", "#6ab04c"],
  "pixelMap": [
    [null, null, 2, 2, null, null, null, null],
    [null, 1, 1, 1, 1, null, null, null],
    [1, 1, 1, 1, 1, 1, null, null]
  ],
  "drainHoleX": 4,
  "drainHoleY": 7
}
```

## Drain Engine

### Drain Tick

One drain tick attempts to drain the pixel at the hole.

Algorithm:

1. Read holeColor from PixelGrid at DrainHole.
2. If holeColor is null, apply gravity and check again.
3. Get activeTube from TubeCarousel.
4. If activeTube.colorIndex != holeColor, stop and return blocked result.
5. Remove the hole pixel from the grid.
6. Increase activeTube.collectedCount.
7. Apply gravity to the grid.
8. Check whether the active tube is complete.
9. Check whether all pixels are drained.
10. Return DrainResult.

### Auto Drain

When active tube color matches the hole color, the engine can continue ticking at a fixed drain speed.

When the hole color changes, auto-drain pauses until the player changes the active tube.

## Gravity Resolver

MVP should use grid-based gravity, not a full physics engine.

Recommended first implementation:

- After a pixel is removed, apply vertical gravity per column.
- In each column, non-empty pixels fall downward into empty cells.
- Preserve horizontal position.

This is simple, predictable, and easy to test.

Later experiments can add sideways collapse or sand-like diagonal movement, but MVP should stay deterministic.

## Tube Selection Controls

Supported controls:

- Swipe left/right to rotate tube carousel
- Optional left/right buttons
- Optional direct tap on visible tube

MVP can start with left/right buttons plus direct tap.

## Completion Rules

A color tube is complete when:

- collectedCount == targetCount for that color

A stage is complete when:

- all tubes are complete
- or the pixel grid has no remaining pixels

Both should be true in a valid stage.

## Star Rating

Possible first version:

- 3 stars: cleared under target rotation count
- 2 stars: cleared under relaxed rotation count
- 1 star: cleared

Alternative later metrics:

- clear time
- number of tube switches
- number of hints used

## Photo Puzzle Mode

### Flow

1. Select image from gallery.
2. Crop to square.
3. Resize to target resolution.
4. Extract palette with limited color count.
5. Quantize image to palette.
6. Build initialPixelMap.
7. Count pixels per color to create ColorTube target counts.
8. Start one-hole drain puzzle.
9. Save generated puzzle metadata locally if needed.

### Suggested Options

- Easy: 16x16, 6 colors
- Normal: 24x24, 8 colors
- Hard: 32x32, 12 colors
- Master: 40x40, 16 colors

MVP can start with only one automatic option.

## Image Processing Notes

The photo-to-puzzle pipeline should preserve readability over accuracy.

Important steps:

- Center crop
- Downscale with nearest-neighbor or controlled sampling
- Palette quantization
- Remove near-duplicate colors
- Optionally boost contrast before quantization
- Avoid too many similar colors in one puzzle
- Ensure color count is suitable for mobile tube selection

## Local Storage

Store:

- Progress
- Settings
- Collection state
- Generated photo puzzle history

Do not store unnecessary personal photo data unless the user explicitly saves it.

## Ads and IAP

Keep behind interfaces:

- AdsService
- PurchaseService

MVP can use fake implementations until release preparation.

## Screens

### HomeStageScreen

Combined home and stage selection screen.

- Logo/title
- Difficulty tabs
- Stage cards
- Photo puzzle button
- Collection button
- Settings button

### PuzzleScreen

- Top status bar: progress, rotations, pause
- Center: framed pixel image
- Bottom center of frame: drain hole
- Below frame: active tube and tube carousel
- Optional next color indicator if enabled

### ClearResultDialog

- Completed original pixel art
- Stars
- Rotation count
- Time
- Next stage
- Retry
- Collection

### CollectionScreen

- Grid of completed images
- Filters by difficulty/theme
- Detail view

### PhotoPuzzleScreen

- Pick image
- Select difficulty option
- Generate puzzle
- Play generated puzzle

## MVP Scope

Build in this order:

1. Static hardcoded pixel grid
2. Drain hole rendering
3. Color tube rendering
4. Tube selection/rotation
5. DrainEngine tick logic
6. Grid gravity resolver
7. Auto-drain while colors match
8. Block/pause when colors mismatch
9. Win detection
10. Clear result dialog
11. JSON stage loading
12. Local progress
13. Stage select
14. Collection basics
15. Photo puzzle prototype

## Testing Focus

- PixelGrid hole color read
- Pixel removal
- Gravity resolution
- Drain tick success
- Drain blocked by color mismatch
- Tube completion
- Stage completion
- Tube carousel rotation
- Stage JSON parsing
- Photo quantization output dimensions

## Non-goals For MVP

- Full physics engine
- Online ranking
- User accounts
- Cloud save
- Social feed
- User-generated puzzle sharing server
- Complex monetization
- Large live-ops system
