# PixoSort Design Plan

## Design Keywords

- Cute
- Clean
- Warm
- Pixel art
- Sand-like
- Satisfying
- Toy-like
- Clear readability

## Visual Direction

PixoSort should feel like a cozy pixel-art puzzle toy where images gently drain like sand through a single hole.

The interface should be bright, soft, and readable. The main visual focus is the framed pixel image collapsing and draining into color tubes.

## Art Style

- Crisp pixel edges
- Simple shading
- Limited color palettes
- No realistic rendering
- No painterly texture
- No 3D look
- Cute object and character silhouettes

## UI Style

Use rounded panels and simple icon buttons while keeping pixel art assets crisp.

Recommended UI feeling:

- Soft background
- Card-based menus
- Large touch targets
- Friendly stage cards
- Clear progress indicators
- Minimal text during gameplay
- One-hand portrait layout

## Color Direction

Use warm neutral backgrounds with colorful puzzle elements.

Suggested palette categories:

- Cream background
- Soft blue accent
- Warm yellow reward color
- Coral highlight
- Mint success color
- Dark navy or brown text

Exact colors can be finalized during UI implementation.

## Typography

Use highly readable fonts for UI text.

Guidelines:

- Avoid tiny text
- Use bold numbers for progress and stars
- Korean and English should both remain readable
- Pixel fonts can be used only for headings or decorative labels if readability is not harmed

## Screen Count Direction

Keep real page count small.

Core pages:

1. HomeStageScreen
2. PuzzleScreen
3. CollectionScreen
4. PhotoPuzzleScreen

Use dialogs or bottom sheets for:

- Clear result
- Pause
- Settings
- Image detail
- Photo puzzle options

## Main Screen Design

### HomeStageScreen

Purpose: Start quickly without too many screens.

Elements:

- Logo/title
- Settings button
- Difficulty tabs: Level 1 to Level 10
- Stage cards for selected difficulty
- Photo puzzle button
- Collection button

The old separate Difficulty Select and Stage Select screens should be merged into this one screen.

### PuzzleScreen

Purpose: Focus on the drain-hole sorting mechanic.

Layout recommendation for portrait mobile:

- Top: progress, rotation count, pause
- Middle: framed pixel art image
- Bottom center of frame: single drain hole
- Below frame: active tube under the hole
- Bottom: tube carousel or tube row
- Optional: left/right rotate buttons

Important visual rules:

- The drain hole must be visually obvious.
- The active tube must align clearly under the hole.
- The current hole pixel color should be easy to read.
- When colors match, pixels should drain smoothly into the tube.
- When colors mismatch, the game should visibly pause or show a soft blocked feedback.

### ClearResultDialog

Purpose: Celebrate color separation completion.

Elements:

- Original completed pixel art preview
- Stage title
- Stars
- Rotation count
- Time
- Next stage button
- Retry button
- Collection button

### CollectionScreen

Purpose: Make completed images feel valuable.

Elements:

- Grid of completed images
- Difficulty/theme filter
- Locked silhouettes
- Detail modal with save/share

### PhotoPuzzleScreen

Purpose: Convert a user photo into a drain puzzle.

Elements:

- Photo picker
- Square preview
- Difficulty option chips
- Pixelated preview
- Generate button

## Puzzle Screen Wireframe

```txt
┌────────────────────┐
│ Progress   Rotations│
├────────────────────┤
│                    │
│   Framed Pixel Art  │
│   image collapses   │
│                    │
│          ▼ hole     │
├──────────●─────────┤
│          ↓          │
│       Active Tube   │
│   ◀  tubes row  ▶   │
└────────────────────┘
```

## Animation Direction

Keep animations short and tactile.

Suggested animations:

- Pixel drain movement from hole to tube
- Tube fill rising or dot count increasing
- Tube carousel snap rotation
- Blocked mismatch pulse
- Color complete sparkle
- Stage clear pop
- Collection unlock stamp

## Pixel Drain Visual

Pixels should feel like chunky grains of color, not liquid.

Recommended treatment:

- The frame holds a pixel grid.
- The bottom-center hole has a small shadow or funnel indicator.
- Drained pixels move downward into the active tube.
- The original image gradually becomes empty and collapses under gravity.
- Tubes fill with a color level or small pixel particles.

## Tube Visual

Each tube corresponds to one color.

Tube display options:

- Color label on tube cap
- Tube fill level based on collected count
- Small count text like 7/18 if needed
- Completion checkmark or sparkle

## Pixel Art Content Direction

The 100 built-in stages should feel like a small world.

Suggested progression:

- Level 1: simple icons
- Level 2: cute objects
- Level 3: food and animals
- Level 4: cat characters
- Level 5: shops and places
- Level 6: travel scenes
- Level 7: cat scenes
- Level 8: busy locations
- Level 9: fantasy scenes
- Level 10: master illustrations

## Mascot Direction

Optional mascot: a small cute cat that appears in menus, hints, and collection unlock moments.

The mascot should not dominate the game. It should support the cozy tone.

## Icon Direction

App icon should communicate:

- Pixel art
- One-hole drain
- Color sorting
- Test tubes

Possible icon concepts:

1. A pixel image draining into a test tube
2. A test tube under a small pixel funnel
3. A cute pixel cat holding a color tube under falling pixels
4. A framed pixel apple with one color stream draining down

## Store Screenshot Direction

Screenshot themes:

1. Watch pixel art drain like sand
2. Match tubes to sort every color
3. 100 cute pixel stages
4. Turn your photo into a puzzle
5. Collect completed pixel art

## Design Constraints

- Must be readable on small phones
- Must work in Korean and English
- Must avoid UI clutter during puzzle play
- Pixel art should remain sharp
- The drain hole and active tube alignment must be clear
- Avoid hard-to-distinguish similar colors in early stages
- Keep controls usable with one hand

## Accessibility Notes

Color-only gameplay can be difficult for some users.

Possible supports:

- Optional symbols on tubes and hole color indicator
- High contrast mode
- Larger tube mode
- Reduced animation option

These can be post-MVP features, but the data model should not prevent them.
