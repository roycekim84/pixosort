# PixoSort

**PixoSort: Pixel Art Puzzle**  
**픽소소트: 도트 컬러 퍼즐**

PixoSort is a Flutter mobile puzzle game where a pixel art image drains through a single hole like sand. Players rotate or select matching color tubes to collect the falling pixels by color.

픽소소트는 도트 그림이 모래시계처럼 아래 중앙 구멍으로 빠져나가고, 플레이어가 같은 색 시험관을 맞춰 도트를 색상별로 분리하는 모바일 퍼즐 게임입니다.

## Core Loop

1. Choose a stage.
2. A pixel art image appears inside a frame.
3. Pixels drain through one bottom-center hole.
4. If the active tube color matches the hole pixel color, matching pixels keep draining into that tube.
5. When the hole pixel color changes, draining stops.
6. Rotate or select the matching tube to continue sorting.
7. Clear the stage by collecting every color into its tube.

## Main Features

- 10 difficulty levels
- 100 built-in stages
- One-hole sand-drain pixel puzzle mechanic
- Color tubes matched to image palette colors
- Photo-to-puzzle bonus mode
- Local collection book
- Offline-first design
- Android and iOS release target

## Documentation

- [Concept Plan](docs/01_concept_plan.md)
- [Implementation Plan](docs/02_implementation_plan.md)
- [Design Plan](docs/03_design_plan.md)
- [Roadmap](docs/04_roadmap.md)
- [Screen Specification](docs/05_screen_spec.md)
- [UI Mockup Reference](docs/design/ui_mockup_reference.md)
- [Codex Agent Instructions](AGENTS.md)
