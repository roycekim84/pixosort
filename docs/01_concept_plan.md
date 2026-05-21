# PixoSort Concept Plan

## Product Name

- English: PixoSort: Pixel Art Puzzle
- Korean: 픽소소트: 도트 컬러 퍼즐

## One-Line Concept

A pixel art image drains through one hole like sand, and players match color tubes to sort every pixel by color.

도트 그림이 모래시계처럼 하나의 구멍으로 빠져나가고, 플레이어가 같은 색 시험관을 맞춰 도트를 색상별로 분리하는 퍼즐 게임.

## Game Overview

PixoSort is a casual mobile puzzle game based on a one-hole pixel drain mechanic.

A pixel art image is placed inside a frame. At the bottom center of the frame, there is one drain hole. Pixels are affected by gravity and gradually move toward this hole. When the color currently sitting on the drain hole matches the active tube color, that pixel drains into the tube. If the next pixel reaching the hole is the same color, it continues draining. When a different color reaches the hole, draining stops until the player rotates or selects the matching tube.

The player clears the stage by collecting all pixels into their matching color tubes.

## Core Fun

- Watching a pixel image crumble and drain like sand
- Matching the correct color tube at the right moment
- Seeing same-colored pixels flow continuously into a tube
- Predicting the next color as the image collapses under gravity
- Completing color tubes one by one
- Turning built-in pixel art or user photos into playable color separation puzzles

## Target Users

- Casual puzzle players
- Players who enjoy color sorting games
- Pixel art and cute illustration fans
- Users who like satisfying sand, drain, and sorting interactions
- Users who want to turn personal photos into simple games

## Key Differentiation

PixoSort is not a standard tube-transfer color sort game.

Instead of moving blocks between tubes, the original pixel image itself is the puzzle material. The image drains through a single hole, and the player sorts the draining pixels by matching the correct tube color.

This creates a stronger visual identity:

> Image -> gravity -> one drain hole -> color tube sorting.

## Main Modes

### Built-in Puzzle Mode

- 10 difficulty levels
- 10 stages per difficulty
- 100 built-in stages total
- Each stage uses a pixel art image and a limited palette
- The number of tubes equals the number of colors
- Completed stages are saved into the collection book

### Photo Puzzle Mode

- User selects a photo
- App crops it to a square
- App converts it to pixel art
- App extracts a limited color palette
- App builds a drainable pixel grid
- User plays the generated one-hole drain puzzle

## Core Gameplay Rules

1. A stage starts with a pixel art image inside a frame.
2. The frame has one drain hole at the bottom center.
3. Pixels are affected by gravity and move toward the drain hole.
4. The active tube is positioned under the hole.
5. If the active tube color matches the hole pixel color, the pixel drains into that tube.
6. If the next hole pixel has the same color, it continues draining.
7. If the next hole pixel has a different color, draining stops.
8. The player rotates or selects another tube to match the new hole color.
9. Each color has one matching tube.
10. A tube is complete when all pixels of that color have been collected.
11. The stage is cleared when every pixel has been collected into the correct tube.

## Tube Structure

- Color count = tube count
- There are no helper or empty tubes in the core mechanic
- Each tube corresponds to one palette color
- Tubes fill according to collected pixel count
- Example: if red appears 18 times in the image, the red tube is complete at 18/18

## Difficulty Structure

Difficulty is controlled by:

- Pixel art resolution
- Color count
- Shape complexity
- Color distribution
- Gravity speed
- Drain speed
- Tube rotation speed
- Whether the next color is previewed
- Whether the game has move, time, or rotation limits

Initial release should mainly use resolution, color count, and image complexity.

## Planned Difficulty Levels

| Level | Resolution | Colors | Theme |
|---:|---|---:|---|
| 1 | 8x8 | 3 | Simple icons |
| 2 | 12x12 | 4 | Cute objects |
| 3 | 16x16 | 5 | Food and animals |
| 4 | 16x16 | 6 | Small characters |
| 5 | 20x20 | 7 | Places and backgrounds |
| 6 | 24x24 | 8 | Travel and scenery |
| 7 | 24x24 | 10 | Character scenes |
| 8 | 32x32 | 12 | Complex scenes |
| 9 | 32x32 | 14 | Advanced illustrations |
| 10 | 40x40 or 48x48 | 16 | Master images |

## Theme Direction

The built-in stages should share a warm and cute pixel-art world.

Suggested themes:

- Food
- Animals
- Cats
- Cat jobs
- Harbors
- Markets
- Travel scenes
- Fantasy locations
- Legendary fish and treasures

## Main Screens

Keep the app screen count small.

Core pages:

- HomeStageScreen: home, difficulty tabs, and stage selection combined
- PuzzleScreen: framed pixel image, drain hole, active tube, tube carousel
- CollectionScreen: completed image collection
- PhotoPuzzleScreen: create a puzzle from a user photo

Dialogs and bottom sheets:

- ClearResultDialog
- SettingsBottomSheet
- PauseDialog
- ImageDetailDialog
- PhotoDifficultyBottomSheet

## Monetization Direction

PixoSort should be playable offline and enjoyable without aggressive monetization.

Possible monetization:

- Rewarded ads for hints or next-color preview
- Rewarded ads for additional photo puzzle generation
- Remove ads purchase
- Premium theme packs
- Unlimited photo puzzle mode
- High-resolution export

## Initial Release Goal

The first release should be a complete small mobile puzzle game for Android and iOS.

Target release contents:

- 100 built-in stages
- One-hole drain sorting mechanic
- Photo puzzle mode
- Local collection book
- Save/share completed images
- Local progress storage
- Optional ads and minimal in-app purchases

## Development Principle

- Offline-first
- No required backend for initial release
- Simple and clear rules
- Short play sessions
- Strong visual satisfaction from draining pixels
- Cute, readable pixel art
- Mobile portrait layout
- One-hand friendly controls
