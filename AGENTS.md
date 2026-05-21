# AGENTS.md

## Project

PixoSort: Pixel Art Puzzle

Korean title: 픽소소트: 도트 컬러 퍼즐

## Goal

Build a Flutter mobile puzzle game where a pixel art image drains through one bottom-center hole like sand. The player rotates or selects the matching color tube under the hole to collect pixels by color. The game targets Android and iOS.

## Core Loop

1. Player selects a stage.
2. A pixel art image appears inside a frame.
3. Pixels move toward one bottom-center drain hole under grid-based gravity.
4. If the active tube color matches the hole pixel color, pixels drain into that tube.
5. Draining continues while the next hole pixel has the same color.
6. If the hole color changes, draining pauses.
7. Player rotates or selects the matching tube to continue.
8. Stage clears when every color has been collected into its matching tube.

## Development Principles

- Keep the project Flutter-first.
- Keep the initial version offline-first.
- Do not add a backend unless explicitly requested.
- Keep code simple and readable.
- Prefer small, testable classes for puzzle logic.
- Keep game rules independent from Flutter widgets.
- Avoid unnecessary dependencies.
- Do not implement monetization until the core game loop is stable.
- Do not add online sharing, accounts, rankings, or cloud save for MVP.
- Do not implement a standard tube-transfer color sort game. PixoSort is a one-hole pixel drain puzzle.

## Important Documents

Read these before implementation:

- docs/01_concept_plan.md
- docs/02_implementation_plan.md
- docs/03_design_plan.md
- docs/04_roadmap.md
- docs/05_screen_spec.md

## Suggested Folder Structure

```txt
lib/
  main.dart
  app/
    pixosort_app.dart
    router.dart
    theme.dart
  core/
    utils/
    constants/
  features/
    puzzle/
      domain/
        models/
        services/
      application/
        drain_controller.dart
      presentation/
        screens/
        widgets/
    stages/
      data/
      application/
      presentation/
    collection/
      domain/
      application/
      presentation/
    photo_puzzle/
      domain/
      application/
      presentation/
    settings/
      presentation/
  infrastructure/
    storage/
    assets/
    image_processing/
assets/
  stages/
  images/
  icons/
test/
  puzzle/
```

This structure may be simplified during early prototyping.

## Core Models To Implement First

- StageDefinition
- PaletteColor
- PixelCell
- PixelGrid
- DrainHole
- ColorTube
- TubeCarousel
- DrainState
- DrainResult
- DrainEngine
- GravityResolver
- DrainController

Puzzle rules must be testable without Flutter UI.

## Core Rules

A stage has one fixed drain hole at the bottom center of the pixel frame.

A drain tick works like this:

1. Read the pixel color at the drain hole.
2. If the hole is empty, apply gravity and check again.
3. Compare the hole color with the active tube color.
4. If colors match, remove that pixel from the grid and add it to the active tube.
5. Apply gravity to the grid.
6. Continue auto-draining while the hole color still matches the active tube.
7. If the hole color differs from the active tube, pause draining.
8. Player must rotate or select the matching tube.

Tube rules:

- Color count equals tube count.
- Each tube corresponds to one palette color.
- A tube is complete when collectedCount equals targetCount for that color.
- The stage is complete when all tubes are complete and the grid has no remaining pixels.

## Gravity Rules For MVP

Use deterministic grid-based gravity, not a full physics engine.

MVP gravity:

- Apply vertical gravity per column.
- Non-empty pixels fall downward into empty cells.
- Preserve horizontal position.

Do not implement diagonal sand flow until after the core prototype feels good.

## Screen Implementation Requirements

Follow docs/05_screen_spec.md for screen structure.

Core pages:

- HomeStageScreen
- PuzzleScreen
- CollectionScreen
- PhotoPuzzleScreen

Supporting overlays:

- ClearResultDialog
- PauseDialog
- SettingsBottomSheet
- ImageDetailDialog
- PhotoDifficultyBottomSheet

Do not split Home, Difficulty Select, and Stage Select into separate pages unless explicitly requested.

## First Implementation Milestone

Implement a playable prototype with:

- One hardcoded stage
- Pixel frame UI
- One bottom-center drain hole
- Tube row or carousel UI
- Active tube selection
- DrainEngine tick logic
- Vertical gravity
- Auto-drain while colors match
- Pause on color mismatch
- Stage clear detection
- Restart button

## Second Implementation Milestone

Add:

- JSON stage loading
- HomeStageScreen with difficulty tabs and stage cards
- ClearResultDialog
- Local progress
- Basic collection
- Basic star rating

## Third Implementation Milestone

Add:

- 100 built-in stages
- Photo puzzle generation
- Save/share completed image
- Release polish

## Testing Requirements

Add unit tests for:

- PixelGrid hole color read
- Pixel removal
- Gravity resolution
- Drain tick success
- Drain blocked by color mismatch
- Tube completion
- Stage completion
- Tube carousel rotation
- Stage JSON parsing

## UI Requirements

- Mobile portrait layout first.
- Make touch targets large enough for mobile.
- Keep the pixel art frame readable.
- Make the drain hole obvious.
- Make active tube alignment under the hole clear.
- Tube color and hole color must be easy to compare.
- Mismatch should show soft blocked feedback.
- Tube completion should animate or visually pop.

## Asset Requirements

Built-in stage data should use JSON.

Prefer compact pixel maps using palette indexes rather than storing full images.

## Do Not Do Yet

- Do not implement traditional tube-to-tube block moving.
- Do not add Supabase/Firebase.
- Do not add user login.
- Do not add remote stage downloads.
- Do not add multiplayer.
- Do not add social feeds.
- Do not add complex live-ops systems.
- Do not add ads before the game is fun.
- Do not add full physics before deterministic grid gravity works.

## Code Style

- Use clear names.
- Keep files focused.
- Prefer immutable models where practical.
- Avoid giant widget files.
- Put pure puzzle logic outside UI.
- Use comments only when the intent is not obvious.

## Build Target

The project should remain suitable for:

- Android release
- iOS release
- Small solo-developer maintenance
