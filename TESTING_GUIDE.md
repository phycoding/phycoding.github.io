# 🎮 Spin Wheel Game - Testing Guide

## How to Run

1. **Open the file** in your web browser:
   - Simply open `index.html` in any modern browser
   - Chrome, Firefox, Safari, Edge all supported

2. **First Time Setup**:
   - Browser will ask for location permission
   - Click "Allow" to collect GPS data
   - Click "Block" to skip (data collection will continue without location)

## Features to Test

### 1. **Spin the Wheel** 🎯
- Click the big gold button "🎯 SPIN THE WHEEL"
- Watch the smooth spinning animation
- See the prize popup
- Stats update automatically

### 2. **Collected Data** 📊
- After spinning, click **"📊 View Collected Data"**
- See all information collected:
  - Your location (latitude/longitude)
  - Your IP address & geolocation
  - Network connection details
  - Device/browser information
  - Exact timestamp

### 3. **Export Data** 💾
- In the data modal:
  - **"⬇️ Download JSON"** - Save as structured JSON file
  - **"📥 Download CSV"** - Save as spreadsheet file

### 4. **Prize Customization** ⚙️
- Click "⚙️ Customize Prizes"
- Edit:
  - Prize icons (any emoji)
  - Prize names
  - Probability weights (1-100)
- Click "✅ Apply Changes"
- Wheel regenerates with new prizes

### 5. **Statistics** 📈
- **Total Spins**: Count of all spins
- **Wins**: Count of actual prizes won
- **Win Rate**: Percentage of winning spins

### 6. **History** 📜
- Last 10 spins shown with timestamps
- Icon and prize name displayed
- Newest spins at top

## Data Being Collected

### ✅ What Gets Saved
- **Location**: GPS coordinates, accuracy, altitude
- **IP Data**: IP address, city, country, ISP
- **Network**: Connection type, speed, latency
- **Device**: OS, browser, screen size, CPU cores
- **Timestamp**: Exact date/time of spin

### Browser Storage
- All data stored in browser's **IndexedDB**
- Data persists between sessions
- Data is **NOT** sent to any server
- Only visible locally or when exported

## Troubleshooting

### Location Permission Issues
- **Windows**: Check Windows privacy settings → Location
- **Mac**: System Preferences → Security & Privacy → Location Services
- **Mobile**: App settings → Permissions → Location

### IP Data Not Loading
- Requires internet connection
- Uses free `ipapi.co` service
- Takes 2-3 seconds to fetch

### Data Not Saving
- Check if IndexedDB is enabled in browser
- Try a different browser
- Clear browser cache and try again

## Browser Compatibility

✅ **Fully Supported**
- Chrome 45+
- Firefox 42+
- Safari 11+
- Edge 15+
- Opera 32+

⚠️ **Limited Support**
- IE 11 (IndexedDB only, no geolocation API)
- Older mobile browsers

## Privacy Notes

- ✅ All data stored locally
- ✅ No data sent to external servers (except IP lookup API)
- ✅ User controls data with export feature
- ✅ Can be cleared anytime from browser storage

## Developer Features

### Access Data Programmatically
```javascript
// Get all spin data
getAllSpinData().then(data => {
    console.log('All spins:', data);
});

// View in console
F12 or Right-click → Inspect → Console
```

### Clear All Data
```javascript
// In browser console:
indexedDB.deleteDatabase('SpinWheelDB');
location.reload();
```

---

**Enjoy the game! 🎰✨**
