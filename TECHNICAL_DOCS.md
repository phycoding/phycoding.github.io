# 🛠️ Technical Documentation - Spin Wheel Game

## Architecture Overview

```
┌─────────────────────────────────────────┐
│        Spin Wheel Game UI               │
│   (HTML5 + CSS3 + SVG Graphics)         │
└──────────────┬──────────────────────────┘
               │
       ┌───────┴────────┐
       │                │
   ┌───▼────┐      ┌───▼───────────┐
   │ Wheel  │      │ Data Collector │
   │ Engine │      │ Module         │
   └────────┘      └───┬───────────┘
                       │
         ┌─────────────┼─────────────┐
         │             │             │
    ┌────▼──┐    ┌────▼──┐    ┌────▼──┐
    │  GPS  │    │  IP   │    │Network│
    │  Data │    │  Data │    │ Info  │
    └───────┘    └───────┘    └───────┘
         │
    ┌────▼─────────────────┐
    │   IndexedDB Storage   │
    │  (Local Database)     │
    └──────────────────────┘
```

## Core Modules

### 1. **Game Engine**
```javascript
// Main spin logic
spin() - Initiates spin sequence
selectPrize() - Weighted random selection
calculateTargetAngle() - Determines landing position
updateStats() - Updates win/loss count
```

### 2. **Data Collection Module**
```javascript
collectUserData() - Main collection orchestrator
├── getGeolocation() - GPS data
├── getIPAddress() - IP geolocation
├── getNetworkInfo() - Connection details
└── [Browser APIs] - Device information
```

### 3. **Storage Module**
```javascript
saveSpinData() - Saves to IndexedDB
getAllSpinData() - Retrieves all records
viewCollectedData() - Displays in UI
downloadDataAsJSON() - Export to JSON
downloadDataAsCSV() - Export to CSV
```

## Data Collection Implementation

### Geolocation API
```javascript
navigator.geolocation.getCurrentPosition(
    success: returns coordinates + accuracy
    error: permission denied or error
    options: enableHighAccuracy, timeout, maximumAge
)

Returns:
- latitude, longitude
- accuracy (meters)
- altitude, altitudeAccuracy
- heading, speed
```

### IP Geolocation (ipapi.co)
```javascript
Endpoint: https://ipapi.co/json/

Returns:
- ip (public IP address)
- city, region, country
- latitude, longitude
- org (ISP name)
- timezone
```

### Network Information API
```javascript
navigator.connection properties:
- effectiveType: '4g', '3g', '2g', 'slow-4g'
- downlink: effective bandwidth (Mbps)
- rtt: round-trip time (ms)
- saveData: user data saver preference
- type: 'wifi', 'cellular', 'bluetooth', 'ethernet'
```

### Browser/Device APIs
```javascript
navigator.userAgent - Full browser/OS string
navigator.language - User's preferred language
navigator.cookieEnabled - Cookie support
navigator.onLine - Connection status
navigator.hardwareConcurrency - CPU core count
navigator.deviceMemory - RAM (GB)
navigator.platform - OS name

window.screen:
- width, height - Screen resolution
- availWidth, availHeight - Available space
- colorDepth - Color depth (bits)
- pixelDepth - Pixel depth

Intl.DateTimeFormat().resolvedOptions().timeZone
- User's timezone
```

## Database Schema (IndexedDB)

### Object Store: "spins"
```javascript
{
  id: Number (timestamp),
  timestamp: String (ISO 8601),
  prize: Object {
    name: String,
    icon: String,
    weight: Number,
    color: String
  },
  userData: Object {
    timestamp: String,
    userAgent: String,
    language: String,
    timezone: String,
    screenResolution: String,
    devicePixelRatio: Number,
    cookiesEnabled: Boolean,
    onLine: Boolean,
    platform: String,
    hardwareConcurrency: Number/String,
    deviceMemory: Number/String,
    
    location: Object {
      latitude: Number,
      longitude: Number,
      accuracy: Number,
      altitude: Number,
      altitudeAccuracy: Number,
      heading: Number,
      speed: Number
      // OR { error: String } if denied
    },
    
    ip: Object {
      ip: String,
      city: String,
      region: String,
      country: String,
      countryCode: String,
      latitude: Number,
      longitude: Number,
      isp: String,
      timezone: String
      // OR { error: String } if failed
    },
    
    network: Object {
      effectiveType: String,
      downlink: Number,
      rtt: Number,
      saveData: Boolean,
      type: String
      // OR { error: String } if unavailable
    }
  }
}
```

## API Calls Made

### 1. Geolocation API
- **Timing**: On spin click
- **Sync**: User grants permission
- **Fallback**: Continues if denied
- **Cost**: None

### 2. IP API (ipapi.co)
- **Timing**: On spin click (async)
- **Endpoint**: `https://ipapi.co/json/`
- **Method**: GET
- **Response Time**: 2-3 seconds
- **Cost**: Free (no API key required)
- **Limit**: ~1000 requests/day

### 3. Browser APIs (No Network)
- All executed locally
- No external calls
- Instant response

## CSS Features

### Animations Used
```css
@keyframes slideIn - Container entrance
@keyframes float - Background particles
@keyframes pulse - Center circle pulse
@keyframes bounce - Modal icons
@keyframes fadeIn - Modal background
@keyframes modalBounce - Modal entrance
@keyframes confetti-fall - Confetti particles
```

### Responsive Breakpoints
```css
< 768px:
  - Reduced padding
  - Smaller text sizes
  - Single column stats
  - Smaller wheel
```

### Gradient Effects
```css
Title: Linear gradient (Gold → Red)
Stats: Gradient background with shadows
Button: Gradient with shine effect
Cards: Subtle gradient backgrounds
```

## JavaScript Features Used

### ES6+ Features
```javascript
- Arrow functions () => {}
- Template literals `${var}`
- Destructuring { prop } = obj
- Spread operator ...array
- Promise/async-await
- Object/Array methods (map, reduce, etc.)
```

### Browser APIs
```javascript
- Fetch API - IP data
- Geolocation API - GPS
- IndexedDB - Database
- LocalStorage - Settings
- Navigator - Device info
- Window/Screen - Display info
```

## Performance Considerations

### Optimizations
- CSS transitions instead of JS animations
- Debounced data collection
- Efficient IndexedDB queries
- Minimal DOM manipulation

### Load Time
- HTML/CSS: Inline (no external files)
- JS: Vanilla JS (no frameworks)
- Total: < 50KB uncompressed

### Storage
- IndexedDB: Unlimited (usually)
- LocalStorage: ~5-10MB
- Each record: ~2-3KB

## Error Handling

### Graceful Degradation
1. Location denied → Continue without it
2. IP API fails → Continue without IP
3. Network info unavailable → Store "N/A"
4. IndexedDB fails → Log to console
5. Any error → Still complete the spin

## Security Considerations

### ✅ Safe Practices
- All data stored locally
- No authentication required
- No server communication (except IP API)
- User controls data export
- No cookies for tracking

### ⚠️ Considerations
- Geolocation reveals location
- IP address is public data
- Device fingerprinting possible
- User should review privacy

### 🔒 Recommendations
- Show privacy notice on load
- Allow opt-out of geolocation
- Provide data download
- Enable data deletion

## Browser Storage Limits

```
LocalStorage: ~5-10MB per domain
IndexedDB: 
  - Chrome: 50% of available disk
  - Firefox: 10GB
  - Safari: 50MB-5GB
  - Edge: Similar to Chrome
```

## Testing Checklist

- [ ] Spin animation smooth
- [ ] Prize selection random
- [ ] Location permission prompt works
- [ ] IP data fetches correctly
- [ ] Data saves to IndexedDB
- [ ] View data modal opens
- [ ] JSON export works
- [ ] CSV export works
- [ ] Stats calculate correctly
- [ ] Responsive on mobile
- [ ] No console errors

## Deployment Notes

1. **HTTPS Required**
   - Geolocation API requires secure context
   - File:// protocol works but limited

2. **CORS Headers**
   - ipapi.co allows CORS requests
   - No CORS issues expected

3. **Browser Support**
   - IndexedDB: 95%+ modern browsers
   - Geolocation: 95%+ modern browsers
   - Network API: 80%+ browsers

4. **Privacy Headers** (Recommended)
   ```
   Permissions-Policy: geolocation=*
   X-Content-Type-Options: nosniff
   ```

## Future Enhancements

- [ ] Backend database (Firebase, PostgreSQL)
- [ ] User authentication
- [ ] Leaderboards
- [ ] Analytics dashboard
- [ ] Real-time notifications
- [ ] Multiplayer mode
- [ ] Advanced data visualization
- [ ] Admin panel

---

**Version**: 1.0.0  
**Last Updated**: 2026-01-05  
**Status**: Production Ready ✅
