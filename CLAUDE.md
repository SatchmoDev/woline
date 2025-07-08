# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Ethiopia security visualization project that creates an animated map showing threat incidents across three specific woredas (administrative districts): Bugna, Gaz Gibla, and Dehana. The visualization displays a timeline-driven animation with incident counters and color-coded threat levels.

## Architecture

### Core Components

**Single-page application (`index.html`)**
- Self-contained HTML file with embedded CSS and JavaScript
- Uses Mapbox GL JS for map rendering and animations
- Implements a sequential animation system with precise timing controls

**Data Sources**
- `data/woreda.geojson`: Administrative boundaries for Ethiopian woredas
- `data/fake.geojson`: Simulated security incident data with timestamps, event types, coordinates, and threat colors (red/yellow)
- `token.js`: Contains Mapbox API access token

### Animation Sequence Architecture

The application follows a carefully orchestrated 6-step animation sequence:
1. **Initial view**: Full Ethiopia map (5-second hold)
2. **Zoom transition**: Animated zoom to target coordinates [38.8089, 12.18] at zoom level 9
3. **UI appearance**: Timeline and three tally boxes fade in
4. **Timeline animation**: 25-second data-driven progression with real-time incident counting and woreda coloring
5. **Random finale**: 30% of all woredas randomly colored (10% red, 20% yellow) representing broader threat landscape
6. **Final zoom out**: Return to full Ethiopia view showing the randomized threat distribution

### Color Logic System

**Time-based threat decay model:**
- Red events trigger 30-day red periods, followed by 20-day yellow periods
- Yellow events trigger 20-day yellow periods
- Colors fade to transparent after decay periods expire
- Flash effects indicate new events in already-colored woredas

**Layer management:**
- Specific woreda layers handle animation-phase coloring
- All-woredas layer handles final random distribution
- Proper layer ordering prevents color bleeding/mixing

## Data Structure

**Event properties:**
- `event_date`: ISO timestamp for temporal positioning
- `event_type`: Six categories (Intertribal Conflict, Kidnapping, Disaster, Political Tension, Protests, Military Action)
- `color`: "red" or "yellow" indicating threat severity
- `coordinates`: [longitude, latitude] for woreda matching

**Woreda matching:**
Uses coordinate proximity matching with 0.001-degree tolerance to associate events with specific woredas.

## Configuration

**Critical coordinates:**
- Ethiopia center: [40.432665, 9.198629] at zoom 5.5
- Target center: [38.8089, 12.18] at zoom 9
- Woreda centers defined in `WOREDA_CONFIGS`

**Timing constants:**
All animation timings centralized in `TIMING` object for easy adjustment. Key durations: 5s initial, 25s timeline, 3s transitions.

## Development

**Running the application:**
Serve the directory with any HTTP server (required for CORS-compliant GeoJSON loading):
```bash
python -m http.server 8000
# or
npx serve .
```

**MapBox dependency:**
Requires valid Mapbox access token in `token.js`. The application uses a custom map style: `mapbox://styles/studavid/cmcmsfdcd00el01s03dabfyoy`

**Recording setup:**
Designed for OBS screen capture with 1920x1080 resolution. Animation runs approximately 35-40 seconds total for complete capture.

## Key Implementation Notes

**State management:**
- `animationActive` flag controls color updates during timeline phase
- `woredaState` tracks last colors and flash states to prevent conflicts
- `tallyCounts` maintains real-time incident totals per woreda

**Performance considerations:**
- Color updates throttled to 200ms intervals during animation
- Uses `requestAnimationFrame` for smooth timeline progression
- Efficient data-driven styling for random woreda coloring phase

**Layer architecture:**
The map uses dual-layer system - specific woreda layers for animation phase, single all-woredas layer for finale. Proper clearing prevents color mixing that could create unintended orange appearances.