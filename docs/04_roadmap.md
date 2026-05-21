# PixoSort Roadmap

## Phase 0: Planning

Goal: Define the one-hole drain puzzle clearly before implementation.

Tasks:

- Finalize concept plan
- Finalize implementation plan
- Finalize design plan
- Create AGENTS.md for Codex implementation
- Decide initial Flutter project structure

Exit criteria:

- Documentation exists in the repository
- Core drain-hole game loop is clear
- MVP scope is fixed

## Phase 1: Prototype

Goal: Prove the one-hole pixel drain mechanic.

Tasks:

- Create Flutter project
- Implement core models: StageDefinition, PixelGrid, DrainHole, ColorTube, TubeCarousel, DrainState
- Render one hardcoded pixel grid inside a frame
- Render one bottom-center drain hole
- Render color tubes under the frame
- Implement tube selection or rotation
- Implement DrainEngine tick logic
- Implement vertical grid gravity
- Drain pixels while active tube color matches hole color
- Pause drain when active tube color does not match hole color
- Detect stage clear when all pixels are collected

Exit criteria:

- One hardcoded stage can be played from start to clear
- Pixels drain through one hole like sand
- Matching tube color allows continuous draining
- Mismatched tube color pauses draining

## Phase 2: MVP Core

Goal: Build the playable stage-based game.

Tasks:

- Load stage data from JSON assets
- Add HomeStageScreen with difficulty tabs and stage cards
- Add PuzzleScreen polish
- Add ClearResultDialog
- Add local progress save/load
- Add basic star rating using rotation count or clear time
- Add restart
- Add 30 test stages across 3 difficulty levels
- Add basic sound effects for drain, mismatch, and completion

Exit criteria:

- User can select and clear multiple stages
- Progress persists after app restart
- Core game feels complete enough for internal testing

## Phase 3: Collection and Content Expansion

Goal: Add collection motivation and enough content.

Tasks:

- Add CollectionScreen
- Add completed image detail view
- Add locked silhouettes
- Expand built-in stages to 100
- Add stage thumbnails
- Add level progression rules
- Add polished animations

Exit criteria:

- 100 built-in stages exist
- Completed stages are stored in the collection
- Game has a complete casual puzzle feel

## Phase 4: Photo Puzzle Mode

Goal: Add personalized replay value.

Tasks:

- Add image picker flow
- Add square crop flow
- Add resize-to-pixel-grid logic
- Add palette extraction
- Add color quantization
- Build a drainable pixel grid from the photo
- Create color tubes based on palette counts
- Add photo puzzle result save/share
- Add safeguards for overly complex images

Exit criteria:

- User can select a photo and play it as a generated one-hole drain puzzle
- Generated puzzles are reasonably readable
- Photo mode does not require a backend

## Phase 5: Release Preparation

Goal: Prepare Android and iOS release.

Tasks:

- Add app icon
- Add splash screen
- Add store screenshots
- Add Korean and English app metadata
- Add privacy policy
- Add terms if needed
- Add ads only if the UX remains clean
- Add remove ads purchase if monetization is included
- Test on multiple device sizes
- Optimize performance
- Run Android release build
- Run iOS release build

Exit criteria:

- App is ready for Google Play and App Store submission
- No critical UX or crash issues remain

## Phase 6: Post Launch

Goal: Improve based on real usage.

Possible tasks:

- Daily puzzle
- More theme packs
- More photo puzzle options
- High-resolution export
- GIF drain animation export
- Cloud backup
- Accessibility symbols for colors
- Extra cat mascot interactions
- Seasonal stages
- Advanced sand-like diagonal gravity mode

## Priority Rule

Always protect the core loop first:

> Pixel image -> one drain hole -> matching color tube -> color-separated completion.

Do not add large systems until this loop feels satisfying.
