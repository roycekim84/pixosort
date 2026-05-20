# PixoSort Roadmap

## Phase 0: Planning

Goal: Define the game clearly before implementation.

Tasks:

- Finalize concept plan
- Finalize implementation plan
- Finalize design plan
- Create AGENTS.md for Codex implementation
- Decide initial Flutter project structure

Exit criteria:

- Documentation exists in the repository
- Core game loop is clear
- MVP scope is fixed

## Phase 1: Prototype

Goal: Prove the core puzzle loop.

Tasks:

- Create Flutter project
- Implement basic models: StageDefinition, Tube, PuzzleState
- Render tubes and color blocks
- Implement tap-to-move tube controls
- Implement move validation
- Implement win detection
- Add one hardcoded test stage
- Add simple pixel board preview
- Fill completed colors on the board

Exit criteria:

- One stage can be played from start to clear
- Sorting a color restores that color on the pixel board

## Phase 2: MVP Core

Goal: Build the playable stage-based game.

Tasks:

- Load stage data from JSON assets
- Add difficulty select screen
- Add stage select screen
- Add puzzle screen polish
- Add result screen
- Add local progress save/load
- Add undo
- Add restart
- Add basic star rating
- Add 30 test stages across 3 difficulty levels

Exit criteria:

- User can select and clear multiple stages
- Progress persists after app restart
- Core game feels complete enough for internal testing

## Phase 3: Collection and Content Expansion

Goal: Add collection motivation and enough content.

Tasks:

- Add collection screen
- Add completed image detail view
- Add locked silhouettes
- Expand built-in stages to 100
- Add stage thumbnails
- Add level progression rules
- Add basic sound effects
- Add simple animations

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
- Generate puzzle tubes from photo pixel data
- Add photo puzzle result save/share
- Add safeguards for overly complex images

Exit criteria:

- User can select a photo and play it as a generated puzzle
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
- GIF completion animation
- Cloud backup
- Accessibility symbols for colors
- Extra cat mascot interactions
- Seasonal stages

## Priority Rule

Always protect the core loop first:

> Sort colors -> restore pixel art -> collect the completed image.

Do not add large systems until this loop feels satisfying.
