# PixoSort Design Plan

## Design Keywords

- Cute
- Clean
- Warm
- Pixel art
- Toy-like
- Light puzzle game
- Clear readability

## Visual Direction

PixoSort should feel like a cozy pixel-art puzzle toy rather than a heavy competitive game.

The interface should be bright, soft, and readable. Pixel art is the main reward, so the UI must not overpower the stage image.

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
- Use bold numbers for move count and stars
- Korean and English should both remain readable
- Pixel fonts can be used only for headings or decorative labels if readability is not harmed

## Main Screen Design

### Home

Purpose: Give immediate access to play.

Elements:

- Logo/title
- Main start button
- Photo puzzle button
- Collection button
- Settings button
- Small animated pixel art mascot or stage preview

### Difficulty Select

Purpose: Show 10 levels clearly.

Elements:

- Level cards
- Difficulty label
- Clear count, e.g. 7/10
- Lock state
- Theme thumbnail

### Stage Select

Purpose: Pick one of 10 stages in a level.

Elements:

- Stage card grid
- Image silhouette or completed thumbnail
- Star count
- Clear state

### Puzzle Screen

Purpose: Focus on sorting and restoration.

Layout recommendation:

- Top: move count, undo, hint, restart
- Middle: pixel art board
- Bottom: tubes

Important:

- Tube blocks must be visually clear.
- Current selected tube should have a clear highlight.
- Completed colors should create satisfying board animation.

### Result Screen

Purpose: Celebrate the restored image.

Elements:

- Completed pixel art large preview
- Stage title
- Stars
- Move count
- Time
- Save/share button
- Next stage button

### Collection

Purpose: Make completed images feel valuable.

Elements:

- Grid of restored images
- Difficulty/theme filter
- Locked silhouettes
- Detail modal with save/share

## Animation Direction

Keep animations short and tactile.

Suggested animations:

- Tube select bounce
- Block move arc or slide
- Invalid move shake
- Color completion sparkle
- Pixel fill wave
- Stage clear pop
- Collection unlock stamp

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
- Color sorting
- Puzzle

Possible icon concepts:

1. A test tube with stacked pixel colors forming a small cat face
2. A pixel palette with sorted color blocks
3. A cute pixel cat holding color tubes
4. A square pixel image partially restored with color tubes below

## Store Screenshot Direction

Screenshot themes:

1. Sort colors, reveal pixel art
2. 100 cute stages
3. Turn your photo into a puzzle
4. Collect restored pixel art
5. Easy to play, satisfying to complete

## Design Constraints

- Must be readable on small phones
- Must work in Korean and English
- Must avoid UI clutter during puzzle play
- Pixel art should remain sharp
- Use consistent spacing and rounded card layout
- Avoid hard-to-distinguish similar colors in early stages

## Accessibility Notes

Color-only gameplay can be difficult for some users.

Possible supports:

- Optional color symbols on blocks
- High contrast mode
- Larger tube mode
- Reduced animation option

These can be post-MVP features, but the data model should not prevent them.
