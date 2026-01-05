# ⚡ Quick Reference Guide

## 🚀 Getting Started in 30 Seconds

1. **Open** → `index.html` in your browser
2. **Allow** → Location permission (or click "Block")
3. **Click** → "🎯 SPIN THE WHEEL"
4. **View** → "📊 View Collected Data"
5. **Export** → Download JSON or CSV

## 🎮 Game Controls

| Action | What Happens |
|--------|--------------|
| Click SPIN button | Collects data → Spins wheel → Shows result |
| Click Customize | Edit prizes and probabilities |
| Click View Data | Shows all collected spins |
| Click Download | Exports to JSON or CSV |

## 📊 Data Collection Timeline

```
Button Click
    ↓
Request Location (2 options)
├─ Allow → Get GPS data ✓
└─ Block → Continue anyway
    ↓
Fetch IP Address → Takes 2-3 seconds
    ↓
Get Network Info → Instant
    ↓
Collect Device Info → Instant
    ↓
SPIN THE WHEEL → 4 second animation
    ↓
Show Result → Win or Try Again
    ↓
Save to IndexedDB → Timestamp + All Data
```

## 🎯 Prize Customization

### Steps
1. Click "⚙️ Customize Prizes"
2. Edit fields:
   - **Icon**: Any emoji (📱, 🎁, etc.)
   - **Name**: Prize name text
   - **Weight**: Probability (1-100)
3. Click "✅ Apply Changes"
4. Wheel updates instantly

### Weight Explanation
```
Weight 5   = 5% chance (rare)
Weight 20  = 20% chance (common)
Weight 50  = 50% chance (very common)
Weight 100 = 100% chance (if only option)
```

## 📂 File Structure

```
index.html              Main game (self-contained, 1252 lines)
README.md              Overview and quick start
FEATURES.md            Detailed feature list
CHANGES.md             Before/after comparison
TESTING_GUIDE.md       How to test and troubleshoot
TECHNICAL_DOCS.md      Development documentation
```

## 💾 Data Storage Locations

### 1. **IndexedDB** (Main Database)
- **Database Name**: SpinWheelDB
- **Object Store**: spins
- **Capacity**: Unlimited (usually 50%+ of disk)
- **Location**: Browser-specific
- **Access**: View Data button in app

### 2. **localStorage** (Stats Only)
- **Key**: spinWheelStats
- **Data**: { totalSpins, totalWins }
- **Capacity**: ~5-10MB
- **Persists**: Yes, across sessions

## 🌍 What Gets Collected

```
├─ Location 🌍
│  ├─ Latitude/Longitude
│  ├─ Accuracy (meters)
│  ├─ Altitude (if available)
│  ├─ Heading/Speed (if available)
│  
├─ IP Address 🌐
│  ├─ Public IP
│  ├─ City/Country
│  ├─ ISP/Organization
│  ├─ Timezone
│  
├─ Network 📡
│  ├─ Connection type
│  ├─ Speed (Mbps)
│  ├─ Latency (ms)
│  ├─ Data saver mode
│  
├─ Device 💻
│  ├─ OS/Browser
│  ├─ Screen resolution
│  ├─ CPU cores
│  ├─ Device memory
│  ├─ Language/Timezone
│  
└─ Timestamp ⏰
   └─ Exact spin time
```

## 🔐 Privacy Checklist

- [ ] Understand what's being collected
- [ ] Review location sharing
- [ ] Check your privacy settings
- [ ] Download your data regularly
- [ ] Delete data if not needed

## 🐛 Troubleshooting Quick Fixes

### Problem: Location not working
**Solution**: 
- Check browser location permission
- Verify HTTPS connection
- Try different browser
- Restart browser

### Problem: IP data missing
**Solution**:
- Check internet connection
- Wait 3 seconds for API
- Refresh page
- Disable VPN/proxy

### Problem: Data not saving
**Solution**:
- Enable JavaScript
- Clear browser cache
- Try different browser
- Check storage quota

### Problem: Wheel not spinning
**Solution**:
- Refresh page
- Check console (F12)
- Clear cache
- Try different browser

## 📱 Keyboard Shortcuts

- **F12** → Open Developer Tools
- **Ctrl+Shift+I** → Inspect Element
- **Ctrl+Shift+Delete** → Clear Browsing Data
- **Enter** → Click focused button

## 🎨 Customization Tips

### Change Button Color
Edit in HTML (search for `spin-button`):
```css
background: linear-gradient(135deg, #YOUR_COLOR1, #YOUR_COLOR2);
```

### Change Background
Edit body background-color:
```css
background: linear-gradient(135deg, #COLOR1 0%, #COLOR2 100%);
```

### Add More Prizes
In JavaScript, add to `prizes` array:
```javascript
{ name: 'Your Prize', icon: '🎁', weight: 25, color: '#ff8b94' }
```

## 📊 Data Analysis

### View in Browser
1. Click "📊 View Collected Data"
2. See all records formatted
3. Copy and paste data

### Export to Excel
1. Click "📥 Download CSV"
2. Open downloaded file
3. Use in Excel/Sheets

### Export to JSON
1. Click "⬇️ Download JSON"
2. Use in programming
3. Process with scripts

## 🎯 Analytics Insights

### Statistics Shown
- **Total Spins**: Game session length
- **Wins**: Success rate
- **Win Rate**: Percentage of wins
- **Prize Distribution**: Most/least won
- **Player Locations**: Geographic spread
- **Device Types**: What players use
- **Network Quality**: Connection types

## 💡 Pro Tips

1. **Export regularly** → Download data weekly
2. **Clear old data** → Remove records you don't need
3. **Test permissions** → Try denying location
4. **Monitor network** → See how players connect
5. **Analyze locations** → Find player demographics
6. **Track engagement** → Monitor spin frequency

## 🔗 API Endpoints Used

```
Browser APIs (No external calls)
├─ navigator.geolocation → GPS
├─ navigator.connection → Network
├─ navigator.userAgent → Browser
└─ window.screen → Display

External API (1 call per spin)
└─ https://ipapi.co/json/ → IP geolocation
   (Free, 1000 requests/day limit)
```

## 📞 Support Resources

- **FEATURES.md** → What can the game do?
- **TESTING_GUIDE.md** → How do I use it?
- **TECHNICAL_DOCS.md** → How does it work?
- **README.md** → Quick overview
- **Browser Console** → Error messages (F12)

## 🎮 Game Rules

- **Win**: Land on any prize (except "Try Again")
- **Lose**: Land on "Try Again" or "Better Luck"
- **Probability**: Based on weight values
- **Fair**: No algorithm tricks, true random

## ⏱️ Timing

| Action | Duration |
|--------|----------|
| Data collection | 2-3 seconds |
| Spin animation | 4 seconds |
| Data saving | < 1 second |
| Total per spin | ~6-7 seconds |

## 📈 Performance Metrics

- **Page Load**: Instant (< 50KB)
- **Animations**: Smooth (60 FPS)
- **Data Query**: < 100ms
- **Export**: < 1 second
- **Memory Usage**: ~5-10MB

---

**💡 Pro Tip**: Open browser DevTools (F12) → Console to see advanced options!

**🎰 Ready to play?** Open index.html and start spinning! ✨
