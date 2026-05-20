# PixoSort Implementation Plan

## Tech Stack

- Flutter
- Dart
- Local-first architecture
- No required backend for MVP
- Local persistence for progress and settings

Suggested packages can be decided during implementation, but the first version should avoid unnecessary dependencies.

## Architecture Direction

Use a simple layered structure:

- Presentation: screens, widgets, animations
- Domain: puzzle rules, stage models, progress models
- Application: game controller, stage loading, photo puzzle generation flow
- Infrastructure: local storage, image processing adapters, ads/IAP adapters

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
- pixelMap
- tubeCapacity
- initialTubes
- previewMode

### PixelMap

A 2D grid of palette indexes.

Example:

```json
[
  [0, 0, 1, 1],
  [0, 2, 2, 1],
  [0, 2, 2, 1],
  [0, 0, 1, 1]
]
```

### ColorBlock

Represents one movable color unit in a tube.

Fields:

- colorIndex
- sourcePixelCount

MVP can treat every block as a simple color unit. Later versions can store area size or pixel group metadata.

### Tube

Fields:

- id
- capacity
- blocks

Rules:

- Blocks are stacked bottom to top.
- A block can move only from the top of a tube.
- A block can move into an empty tube or onto the same color.
- Target tube must have enough capacity.

### PuzzleState

Fields:

- stageId
- tubes
- completedColorIndexes
- moveCount
- elapsedTime
- undoStack
- isCompleted

### UserProgress

Fields:

- clearedStageIds
- stageStars
- bestMoveCounts
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

## Puzzle Generation From Pixel Art

For built-in stages:

1. Load palette and pixel map.
2. Count required color blocks.
3. Convert color counts into tube blocks.
4. Shuffle blocks into initial tubes while ensuring the puzzle is solvable.
5. Store or generate initialTubes.

MVP recommendation:

- Pre-generate initialTubes in stage JSON.
- Do not rely on runtime random generation for built-in stages.
- This makes balancing easier and avoids unsolvable puzzles.

## Runtime Puzzle Rules

### Move Validation

A move is valid when:

- Source tube is not empty.
- Destination tube is not full.
- Source and destination are different.
- Destination is empty, or destination top color equals source top color.

### Move Execution

MVP can move one block at a time.

Later enhancement:

- Move consecutive same-color blocks together if the destination has enough space.

### Color Completion

A color is completed when all blocks of that color are gathered into a valid tube group.

MVP rule:

- A tube is complete if it is full and every block has the same color.
- When complete, mark that color as restored.

Advanced rule for later:

- Support colors requiring multiple complete tubes when pixel count is high.

## Pixel Art Restoration

The board uses the stage pixelMap.

Display rules:

- If a color is not completed, render that pixel as hidden, dimmed, or silhouette.
- If a color is completed, render the actual palette color.
- When a color becomes completed, animate all pixels of that color filling in.

## Star Rating

Possible first version:

- 3 stars: cleared under target move count
- 2 stars: cleared under relaxed move count
- 1 star: cleared

Each stage definition can include targetMoveCount later.

## Photo Puzzle Mode

### Flow

1. Select image from gallery.
2. Crop to square.
3. Resize to target resolution.
4. Extract palette with limited color count.
5. Quantize image to palette.
6. Build pixelMap.
7. Generate tubes from palette counts.
8. Start puzzle.
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

### HomeScreen

- Start
- Photo Puzzle
- Collection
- Settings

### DifficultySelectScreen

- Level cards
- Clear counts
- Locked/unlocked state

### StageSelectScreen

- 10 stage cards for selected difficulty
- Preview or silhouette
- Star count

### PuzzleScreen

- Pixel board
- Tube area
- Move count
- Undo
- Hint
- Restart
- Pause/settings

### ResultScreen

- Completed pixel art
- Move count
- Time
- Stars
- Save/share
- Next stage

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

1. Static stage loading
2. Tube rendering
3. Move rules
4. Win detection
5. Pixel board restoration
6. Result screen
7. Local progress
8. Stage select
9. Collection basics
10. Photo puzzle prototype

## Testing Focus

- Move validation
- Undo behavior
- Win detection
- Stage loading
- Completion state
- Local progress save/load
- Photo quantization output dimensions

## Non-goals For MVP

- Online ranking
- User accounts
- Cloud save
- Social feed
- User-generated puzzle sharing server
- Complex monetization
- Large live-ops system
