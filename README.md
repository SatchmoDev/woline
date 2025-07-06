# Woline - Ethiopian Security Incident Visualization Dashboard

A real-time visualization dashboard that displays security incidents across three Ethiopian woredas (administrative districts): Bishoftu, Jimma, and Debre Tabor. The application provides an interactive timeline showing how security situations evolve over time with color-coded threat levels.

## Features

- **Three-Panel Map Display**: Side-by-side visualization of three different woredas
- **Real-Time Timeline Animation**: 35-second animated timeline showing incident progression from June 2024 to June 2025
- **Color-Coded Threat Levels**:
  - **Red**: High-risk incidents (fatalities ≥ certain threshold) - displayed for 30 days
  - **Yellow**: Medium-risk incidents or red incidents aging out - displayed for 20 additional days
  - **Transparent**: No active threats
- **Interactive Incident Tallies**: Real-time counters for each incident type:
  - Intertribal Conflict
  - Kidnapping
  - Disaster
  - Political Tension
  - Protests
  - Military Action
- **Visual Flash Effects**: White flash when new incidents occur in already-active threat areas
- **Responsive Design**: Optimized for full-screen dashboard display

## Technology Stack

- **Frontend**: Vanilla HTML, CSS, and JavaScript
- **Mapping**: Mapbox GL JS v3.12.0
- **Geospatial Processing**: Turf.js v6
- **Data Format**: GeoJSON for both administrative boundaries and incident data

## Quick Start

1. Clone or download this repository
2. Create a `token.js` file in the root directory with your Mapbox access token:
   ```javascript
   const MAPBOX_ACCESS_TOKEN = "your-mapbox-token-here"
   ```
3. Ensure you have a web server to serve the files (due to CORS restrictions on local file access)
4. Open `index.html` in a web browser
5. The dashboard will automatically begin the timeline animation after map initialization

### Using a Local Web Server

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js (if you have http-server installed)
npx http-server

# Using PHP
php -S localhost:8000
```

Then navigate to `http://localhost:8000` in your browser.

## Data Structure

### Administrative Boundaries (`data/woreda.geojson`)

Contains the geographic boundaries for Ethiopian woredas with properties including:

- `id`: Unique woreda identifier

### Incident Data (`data/fake.geojson`)

Contains security incident points with properties including:

- `event_id`: Unique incident identifier
- `event_date`: Date of incident (YYYY-MM-DD format)
- `event_type`: Category of security incident
- `fatalities`: Number of casualties
- `color`: Threat level indicator ("red" or "yellow")
- `coordinates`: [longitude, latitude] of incident location

## Configuration

Key configuration constants in the JavaScript code:

```javascript
const TIMING_CONSTANTS = {
  timelineAnimationDuration: 35000, // 35 seconds total animation
  redPeriodDays: 30, // Days to show red threat level
  yellowOnlyPeriodDays: 20, // Additional days for yellow level
  flashDuration: 200, // Flash effect duration in ms
}
```

### Mapbox Configuration

- Custom Mapbox style: `mapbox://styles/studavid/cmcmsfdcd00el01s03dabfyoy`
- Access token should be placed in `token.js` (excluded from version control)

## Project Structure

```
woline/
├── index.html          # Main application file
├── token.js            # Mapbox access token (create this file)
├── data/
│   ├── woreda.geojson  # Administrative boundary data
│   ├── fake.geojson    # Security incident data
│   └── seal.png        # Watermark logo
├── favicon.ico         # Browser icon
├── .gitignore          # Git ignore file
└── README.md           # This file
```

## Security and Privacy

This dashboard is designed for defensive security analysis and incident monitoring. The data includes:

- Geographic incident locations
- Incident types and severity levels
- Timeline information for threat assessment

## Browser Compatibility

- Chrome/Chromium 60+
- Firefox 55+
- Safari 12+
- Edge 79+

Requires WebGL support for Mapbox GL JS functionality.

## Development Notes

- The application uses a 35-second animation cycle to represent approximately 1 year of data
- Color transitions follow a specific timeline: Red (30 days) → Yellow (20 days) → Transparent
- Maps automatically transition from a country-wide view to individual woreda focus over 4 seconds
- Incident tallies update in real-time during timeline playback

## Performance Considerations

- Timeline updates are throttled to 200ms intervals for smooth animation
- Map transitions use eased animations for visual appeal
- Color updates are batched to minimize rendering overhead

## License

This project is provided as-is for educational and defensive security purposes.
