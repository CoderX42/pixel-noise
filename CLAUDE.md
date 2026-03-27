# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

PixelNoise is a pixel-art style ambient sound generator with a Minecraft/retro 8-bit game UI aesthetic. It uses Web Audio API for pure synthesis (no external audio files) and Canvas for pixel particle animations.

## Key Files

- `ui/Antigravity/design-spec-v2.md` - Complete design specification in Chinese (grid system, color palette, typography, components, animations, responsive rules)
- `frontend-design/SKILL.md` - Frontend design guidelines for creating distinctive, production-grade interfaces
- `ui/Antigravity/ui-v5.html` - Latest UI implementation (v5)

## Architecture

### Design System
- **Grid**: 8×8px base, 16×16px icons, 32×32px/64×64px blocks
- **Fonts**: Press Start 2P (logo/titles), VT323 (body/numbers)
- **Colors**: Stone gray (#C6C6C6), Grass green (#5C8C58), Diamond blue (#6B8E9F), Lava orange (#E8833A), Coal black (#2D2D2D)
- **Borders**: 2px solid #2D2D2D with inset highlights/shadows for 3D block effect

### Audio Engine
Pure Web Audio API synthesis - no external audio files:
| Sound | Synthesis |
|-------|-----------|
| Rain | Pink noise + 1000Hz lowpass |
| Wind | Pink noise + 400Hz bandpass |
| Snow | Pink noise + 500Hz lowpass × 0.6 |
| Bonfire | Brownian noise + 350Hz lowpass |
| Ocean | Pink noise + lowpass + 0.08Hz LFO |
| White noise | Direct white noise |

### Canvas Particle System
- 48×72 logical resolution, CSS scaled
- 30fps frame rate for retro feel
- Particle styles per sound type (rain drops, wind streaks, snowflakes, flames, waves, static noise)
- Click ripple effects using strokeRect

### Responsive Modes
- **Portrait** (≥500px height): Vertical stack - title bar, canvas, sound grid (horizontal scroll), control bar
- **Landscape** (≤500px): Full-screen canvas with floating title bar, sound drawer slides from left, control bar collapses to bottom strip

### Data Persistence
localStorage key `pxn2` stores: `{ "sound": "rain", "volume": 50, "theme": "day" }`

## Design Guidelines

When modifying or extending this project:
- Maintain the 8-bit blocky aesthetic with proper inset shadows/highlights
- Use pixel fonts (Press Start 2P, VT323) - never generic fonts like Inter or Roboto
- Audio activation requires user interaction (browser autoplay policy)
- Sound cells: 80×96px portrait, 72×76px landscape drawer
- Pixel icons: 16×16 canvas grid drawings
