# AGENTS.md

## Project

PixoSort: Pixel Art Puzzle

Korean title: 픽소소트: 도트 컬러 퍼즐

## Goal

Build a Flutter mobile puzzle game where players sort mixed color blocks into tubes. Completed colors restore parts of a hidden pixel art image. The game targets Android and iOS.

## Core Loop

1. Player selects a stage.
2. Player sorts color blocks between tubes.
3. A completed color fills matching pixels on the pixel art board.
4. All colors completed means the image is restored.
5. The image is saved into the collection.

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

## Important Documents

Read these before implementation:

- docs/01_concept_plan.md
- docs/02_implementation_plan.md
- docs/03_design_plan.md
- docs/04_roadmap.md

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
        puzzle_controller.dart
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
- Tube
- ColorBlock
- PuzzleState
- PuzzleMove
- PuzzleRules
- PuzzleController

Puzzle rules must be testable without Flutter UI.

## Puzzle Rules

A move is valid when:

- Source tube is not empty.
- Destination tube is not full.
- Source and destination are different.
- Destination is empty, or destination top color equals source top color.

MVP should move one top block at a time.

A tube is complete when:

- It is full.
- Every block in it has the same color.

When a color is completed, mark that color as restored on the pixel board.

## First Implementation Milestone

Implement a playable prototype with:

- One hardcoded stage
- Tube UI
- Tap source and destination controls
- Valid move logic
- Win detection
- Pixel board restoration
- Restart button

## Second Implementation Milestone

Add:

- JSON stage loading
- Difficulty select
- Stage select
- Result screen
- Local progress
- Undo
- Basic collection

## Third Implementation Milestone

Add:

- 100 built-in stages
- Photo puzzle generation
- Save/share completed image
- Release polish

## Testing Requirements

Add unit tests for:

- Move validation
- Move execution
- Invalid moves
- Tube completion
- Stage completion
- Undo
- Stage JSON parsing

## UI Requirements

- Make touch targets large enough for mobile.
- Keep the pixel art board readable.
- Keep tube blocks visually distinct.
- Selected tube must have clear feedback.
- Invalid move should show subtle feedback.
- Completed colors should animate or visually pop.

## Asset Requirements

Built-in stage data should use JSON.

Prefer compact pixel maps using palette indexes rather than storing full images.

## Do Not Do Yet

- Do not add Supabase/Firebase.
- Do not add user login.
- Do not add remote stage downloads.
- Do not add multiplayer.
- Do not add social feeds.
- Do not add complex live-ops systems.
- Do not add ads before the game is fun.

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
