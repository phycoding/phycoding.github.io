# Redirect Setup Guide

This site is configured to automatically redirect visitors to a new website.

## How to Configure the Redirect

To update the redirect destination URL, edit `index.html` and modify the following:

### 1. Update the Meta Refresh Tag (Line 7)
```html
<meta http-equiv="refresh" content="3;url=https://www.example.com">
```
Change `https://www.example.com` to your target URL.

### 2. Update the JavaScript Redirect (Line 12)
```javascript
var redirectUrl = 'https://www.example.com';
```
Change `https://www.example.com` to your target URL.

### 3. Update the Manual Link (Line 102)
```html
<a href="https://www.example.com" style="color: #00b98b;">click here</a>
```
Change `https://www.example.com` to your target URL.

## How It Works

The redirect uses two methods for maximum compatibility:

1. **HTML Meta Refresh**: Works in browsers with JavaScript disabled
2. **JavaScript Redirect**: Provides better control and countdown timer

Both methods redirect after 3 seconds, giving users time to read the message and see the countdown. Users can also click the manual link if they don't want to wait.

## Customization Options

### Change Redirect Delay

To change the redirect delay from 3 seconds to something else:

1. Update the meta refresh content: `content="3;url=..."` (change the `3`)
2. Update the JavaScript delay: `var redirectDelay = 3000;` (in milliseconds)
3. Update the countdown timer initial value: `var seconds = 3;`

### Disable Redirect (for testing)

To temporarily disable the redirect:
- Comment out the meta refresh tag
- Comment out or remove the JavaScript redirect code block

## Testing

After making changes, test the redirect by:
1. Opening the page in a browser
2. Verifying the countdown timer works
3. Confirming the redirect happens after the specified delay
4. Testing the manual "click here" link
