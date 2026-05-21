# PixoSort Screen Specification

## Layout Policy

PixoSort is designed as a portrait-first mobile game.

Primary target:

- Mobile portrait orientation
- One-hand friendly controls
- Simple page structure
- Dialogs and bottom sheets instead of extra full pages when possible

Core pages:

1. HomeStageScreen
2. PuzzleScreen
3. CollectionScreen
4. PhotoPuzzleScreen

Supporting overlays:

- ClearResultDialog
- PauseDialog
- SettingsBottomSheet
- ImageDetailDialog
- PhotoDifficultyBottomSheet

## Navigation Map

```txt
HomeStageScreen
  ├─ PuzzleScreen
  │   ├─ ClearResultDialog
  │   └─ PauseDialog
  ├─ CollectionScreen
  │   └─ ImageDetailDialog
  ├─ PhotoPuzzleScreen
  │   └─ PhotoDifficultyBottomSheet
  │       └─ PuzzleScreen
  └─ SettingsBottomSheet
```

## 1. HomeStageScreen

### Purpose

HomeStageScreen combines the title screen, difficulty selection, and stage selection into one compact page.

The player should be able to open the app and start a stage quickly without moving through multiple menus.

### Main Elements

- App title: PixoSort
- Settings button
- Difficulty tabs: Level 1 to Level 10
- Stage card grid for selected difficulty
- Photo Puzzle button
- Collection button
- Optional small mascot or animated pixel preview

### Suggested Layout

```txt
┌────────────────────┐
│ PixoSort        ⚙  │
├────────────────────┤
│ Lv1 Lv2 Lv3 ...    │
├────────────────────┤
│ [01] [02] [03]     │
│ [04] [05] [06]     │
│ [07] [08] [09]     │
│ [10]               │
├────────────────────┤
│ [Photo Puzzle]     │
│ [Collection]       │
└────────────────────┘
```

### Stage Card States

- Locked
- Unlocked but not cleared
- Cleared with 1 to 3 stars
- Current next stage recommendation

### Actions

- Tap difficulty tab: changes visible stage cards
- Tap unlocked stage card: opens PuzzleScreen
- Tap locked stage card: shows small locked feedback
- Tap Photo Puzzle: opens PhotoPuzzleScreen
- Tap Collection: opens CollectionScreen
- Tap Settings: opens SettingsBottomSheet

### Implementation Notes

- Use one screen instead of separate home, difficulty, and stage screens.
- Keep first level immediately playable.
- Store the last selected difficulty locally if useful.

## 2. PuzzleScreen

### Purpose

PuzzleScreen is the main gameplay screen.

It shows the pixel image inside a frame, one bottom-center drain hole, and the color tubes below. The player changes the active tube to match the current hole pixel color.

### Main Elements

- Top status bar
  - Back or pause button
  - Stage title or number
  - Progress percentage
  - Rotation count or time
- Pixel frame
  - PixelGrid
  - Bottom-center drain hole
  - Optional hole color indicator
- Active tube area
  - Tube currently aligned under the hole
- Tube carousel or tube row
  - One tube per palette color
  - Completion state for each tube
- Optional rotate left/right buttons

### Suggested Layout

```txt
┌────────────────────┐
│ II  Stage 1   35%  │
├────────────────────┤
│                    │
│   framed pixel art  │
│   collapsing grid   │
│                    │
│         ▼ hole      │
├─────────●──────────┤
│         ↓           │
│      active tube    │
│  ◀  🧪 🧪 🧪 🧪  ▶  │
└────────────────────┘
```

### Gameplay States

#### Ready

- Stage loaded
- First hole color is visible
- Active tube may or may not match
- Player can rotate/select tube

#### Draining

- Active tube color matches hole pixel color
- Pixels automatically drain into tube at the stage drain speed
- Tube fill count increases
- Pixel grid updates after each drain tick

#### Blocked

- Hole pixel color does not match active tube color
- Drain pauses
- Subtle mismatch feedback is shown
- Player must switch to a matching tube

#### Color Complete

- One tube reaches its target count
- Tube shows completion checkmark or sparkle
- Completed tube remains selectable but should not cause confusion

#### Stage Complete

- All pixels collected
- All tubes complete
- ClearResultDialog opens

### Controls

MVP controls:

- Tap a tube to make it active
- Optional left/right buttons to rotate active tube

Post-MVP controls:

- Swipe left/right to rotate tube carousel
- Haptic feedback on tube snap

### Important Rules To Visualize

- There is exactly one drain hole.
- Only the active tube under the hole can receive pixels.
- Matching color drains automatically.
- Different color stops the flow.
- The player is not moving pixels manually.

### Implementation Notes

- Keep all puzzle logic outside widgets.
- PuzzleScreen should subscribe to DrainController state.
- Rendering should be deterministic from DrainState.
- Do not implement traditional tube-to-tube movement.

## 3. ClearResultDialog

### Purpose

Show completion feedback without navigating to a full result page.

### Main Elements

- Stage clear title
- Completed original pixel art preview
- Stars
- Rotation count
- Clear time
- Buttons:
  - Next Stage
  - Retry
  - Collection
  - Home

### Suggested Layout

```txt
┌────────────────────┐
│ Stage Clear!        │
│                    │
│   completed image   │
│                    │
│      ★ ★ ★          │
│ Rotations: 18       │
│ Time: 00:42         │
│ [Next] [Retry]      │
│ [Collection] [Home] │
└────────────────────┘
```

### Actions

- Next Stage: starts next unlocked stage
- Retry: restarts current stage
- Collection: opens CollectionScreen
- Home: returns to HomeStageScreen

### Implementation Notes

- Use a dialog or bottom sheet, not a separate page.
- Save progress before showing the dialog.
- Unlock next stage before the player leaves the result.

## 4. CollectionScreen

### Purpose

Show completed pixel art images and make stage completion feel collectible.

### Main Elements

- Header with back button
- Difficulty/theme filter
- Grid of collection cards
- Locked silhouettes
- Completed thumbnails
- Star count

### Suggested Layout

```txt
┌────────────────────┐
│ ← Collection        │
├────────────────────┤
│ All Lv1 Lv2 Cat ... │
├────────────────────┤
│ [img] [img] [lock]  │
│ [img] [lock][img]   │
│ [lock][img] [img]   │
└────────────────────┘
```

### Actions

- Tap completed image: opens ImageDetailDialog
- Tap locked image: shows source stage or locked message
- Tap filter: updates grid

### Implementation Notes

- Collection data comes from local progress.
- Use original completed pixel art, not the drained grid state.
- Locked silhouettes should preserve curiosity without revealing too much.

## 5. ImageDetailDialog

### Purpose

Show one completed collection item in detail.

### Main Elements

- Large pixel art preview
- Stage title
- Difficulty
- Stars
- Best rotation count/time
- Save/share button if implemented

### Actions

- Close
- Save image
- Share image
- Replay stage

### Implementation Notes

- Can be a modal dialog or bottom sheet.
- Save/share may be postponed until release preparation.

## 6. PhotoPuzzleScreen

### Purpose

Allow the user to create a one-hole drain puzzle from a personal photo.

### Main Elements

- Header with back button
- Photo picker area
- Square crop/preview area
- Pixelated preview
- Difficulty option
- Generate puzzle button

### Suggested Layout

```txt
┌────────────────────┐
│ ← Photo Puzzle      │
├────────────────────┤
│ [Select Photo]      │
│                    │
│   square preview    │
│                    │
│ Difficulty: Normal  │
│ [Generate Puzzle]   │
└────────────────────┘
```

### Actions

- Tap Select Photo: opens platform image picker
- Tap Difficulty: opens PhotoDifficultyBottomSheet
- Tap Generate Puzzle: converts photo to pixel grid and opens PuzzleScreen

### Difficulty Presets

- Easy: 16x16, 6 colors
- Normal: 24x24, 8 colors
- Hard: 32x32, 12 colors
- Master: 40x40, 16 colors

MVP may support only one preset first.

### Implementation Notes

- Do not upload photos to a server.
- Keep photo processing local.
- Avoid storing original photo unless the user explicitly saves it.
- Use generated pixel data for gameplay.

## 7. PhotoDifficultyBottomSheet

### Purpose

Let the user choose how complex the generated photo puzzle should be.

### Main Elements

- Preset list
- Resolution and color count summary
- Recommended badge if auto-detected
- Confirm button

### Actions

- Select preset
- Confirm selection
- Close without change

## 8. PauseDialog

### Purpose

Pause gameplay and provide safe exit/restart options.

### Main Elements

- Resume
- Restart
- Home
- Settings

### Actions

- Resume: closes dialog
- Restart: asks confirmation if needed, then resets stage
- Home: returns to HomeStageScreen
- Settings: opens SettingsBottomSheet

## 9. SettingsBottomSheet

### Purpose

Provide lightweight settings without a full page.

### Main Elements

- Sound on/off
- Vibration on/off
- Language if needed
- Reduced animation if needed
- Privacy policy link for release
- Remove ads if implemented

### Implementation Notes

- Store settings locally.
- Keep it minimal for MVP.

## Empty, Loading, and Error States

### Loading Stage

- Show a small pixel loading indicator.
- Avoid long loading screens.

### No Collection Items

- Show friendly message: Complete stages to fill your collection.

### Photo Processing Failed

- Show reason if possible.
- Allow selecting another photo.

### Invalid Stage Data

- Show fallback error screen or return to HomeStageScreen.
- Log error in debug builds.

## MVP Screen Scope

The first playable prototype only needs:

1. PuzzleScreen
2. ClearResultDialog

The first app MVP should include:

1. HomeStageScreen
2. PuzzleScreen
3. ClearResultDialog
4. CollectionScreen basic

PhotoPuzzleScreen can be added after the built-in stage loop feels good.

## Final Screen Rule

Avoid screen bloat.

Prefer:

- 4 core pages
- Dialogs/bottom sheets for short tasks
- One portrait-oriented gameplay layout

The player should feel like the whole game is:

> Pick a picture -> drain colors through one hole -> match tubes -> complete the color separation.
