# Ethiopia Security Visualization

An interactive, animated map visualization displaying security incidents across three Ethiopian woredas (administrative districts): Bugna, Gaz Gibla, and Dehana. The visualization presents a timeline-driven animation showing the evolution of threat levels over time, culminating in a broader view of security conditions across Ethiopia.

## Overview

This project creates a cinematic security briefing visualization that:
- Opens with a full map of Ethiopia
- Zooms to focus on three specific woredas in the northern region
- Displays real-time incident counters for six threat categories
- Shows color-coded threat levels (red/yellow) based on recent incident activity
- Concludes with a randomized threat distribution across all of Ethiopia

## Features

### Animated Timeline
- **25-second data progression** through security incidents from 2024-2025
- **Real-time incident counting** across six categories:
  - Intertribal Conflict
  - Kidnapping
  - Disaster
  - Political Tension
  - Protests
  - Military Action

### Dynamic Threat Visualization
- **Time-based color system**: Red indicates recent high-threat incidents, yellow shows moderate threats
- **Threat decay model**: Colors fade over time (red → yellow → transparent)
- **Flash effects**: Visual indicators when new incidents occur in active threat areas

### Geographic Focus
- **Target region**: Northern Ethiopia (coordinates: 38.8089°E, 12.18°N)
- **Administrative units**: Three specific woredas with detailed incident tracking
- **Final overview**: Randomized threat distribution across all Ethiopian woredas

## Quick Start

### Prerequisites
- Web browser with WebGL support
- HTTP server (required for local file serving)
- Mapbox account (token provided)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/ethiopia-security-viz.git
   cd ethiopia-security-viz
   ```

2. **Start a local server**
   ```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js
   npx serve .
   
   # Using any other HTTP server
   ```

3. **Open in browser**
   ```
   http://localhost:8000
   ```

4. **View the animation**
   The visualization starts automatically and runs for approximately 35-40 seconds.

## Data Structure

### Security Incidents (`data/fake.geojson`)
Each incident includes:
- **Timestamp**: Event date for timeline positioning
- **Location**: Coordinates matching specific woredas
- **Event Type**: One of six security categories
- **Threat Level**: Red (high) or Yellow (moderate)
- **Casualties**: Fatality count for severity assessment

### Administrative Boundaries (`data/woreda.geojson`)
Ethiopian administrative district boundaries for geographic visualization.

## Configuration

### Key Settings (in `index.html`)
```javascript
// Target coordinates and zoom level
const TARGET_CENTER = [38.8089, 12.18]
const TARGET_ZOOM = 9

// Animation timing
const TIMING = {
  initialDelay: 5000,        // 5-second opening
  timelineDuration: 25000,   // 25-second progression
  // ... other timing settings
}

// Threat decay periods
redPeriodDays: 30,           // Red threat duration
yellowOnlyPeriodDays: 20,    // Yellow threat duration
```

## Screen Recording

This visualization is optimized for screen capture:

### OBS Studio Setup
1. **Add Browser Source**
   - URL: `http://localhost:8000`
   - Resolution: 1920x1080
   - Enable "Refresh browser when scene becomes active"

2. **Recording Settings**
   - Format: MP4
   - Quality: High (10000+ Kbps)
   - Duration: ~40 seconds for complete animation

3. **Timing**
   - Start recording before page load
   - Animation begins automatically after 5 seconds
   - Full sequence completes in 35-40 seconds

## Technical Architecture

### Built With
- **Mapbox GL JS**: Interactive map rendering and animations
- **Vanilla JavaScript**: No external frameworks
- **GeoJSON**: Standard geographic data format
- **CSS3**: Animations and responsive design

### Key Components
- **Animation Controller**: Orchestrates the 6-step sequence
- **Timeline System**: Manages data progression and UI updates
- **Color State Manager**: Handles threat level visualization
- **Layer Management**: Separate rendering for animation and finale phases

## Browser Compatibility

- Chrome 80+ (recommended)
- Firefox 75+
- Safari 13+
- Edge 80+

WebGL support required for optimal performance.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Acknowledgments

- Ethiopian administrative boundary data
- Mapbox for mapping platform
- Security incident data modeling based on real-world patterns

---

**Note**: This visualization uses simulated data for demonstration purposes. The incident data is generated for educational and presentation use only.