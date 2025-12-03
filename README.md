# Photo Dump

Website for the Photo Dump iOS app.

## Features

- **Universal Links Support**: Handles album-share links that open the iOS app when installed
- **Landing Page**: Shows album invitation page when app is not installed
- **Smart App Banner**: Safari automatically shows download banner
- **Copy Link Functionality**: Users can copy the album link to reopen after installing
- **Flexible URL Support**: Handles both `/joinAlbum/ALBUM_ID` and `/joinAlbum?id=ALBUM_ID` formats

## Setup

### Apple App Site Association

The file `.well-known/apple-app-site-association` needs to be configured with your actual app details:

1. Replace `YOUR_TEAM_ID` with your Apple Developer Team ID
2. Replace `com.photodump.app` with your actual app bundle ID

Example:
```json
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "ABCD123456.com.example.photodump",
        "paths": ["/joinAlbum/*", "/joinAlbum"]
      }
    ]
  }
}
```

### Apple Smart App Banner

In `joinAlbum/index.html`, replace `YOUR_APP_ID` with your actual App Store app ID:

```html
<meta name="apple-itunes-app" content="app-id=YOUR_APP_ID">
```

Also update the App Store link in the same file.

## Deployment

This is a static website that can be hosted on:
- GitHub Pages
- Netlify
- Vercel
- Any static hosting service

### Important Notes

1. **Domain**: The site should be hosted at `https://photo-dump.app`
2. **HTTPS Required**: Universal links only work with HTTPS
3. **Content-Type**: The `.well-known/apple-app-site-association` file must be served with `Content-Type: application/json`
4. **.nojekyll**: This file ensures GitHub Pages serves the `.well-known` directory correctly

### GitHub Pages Setup

1. Enable GitHub Pages in repository settings
2. Set custom domain to `photo-dump.app`
3. Enable HTTPS
4. The `.nojekyll` file ensures proper serving of the `.well-known` directory

### Testing Universal Links

1. Test on a physical iOS device (not simulator)
2. Long-press the link in Messages, Mail, or Safari
3. You should see "Open in [Your App Name]" option
4. Verify the link opens your app correctly

## Album Link Format

The website supports two URL formats:

1. Path-based: `https://photo-dump.app/joinAlbum/ALBUM_ID_HERE`
2. Query-based: `https://photo-dump.app/joinAlbum?id=ALBUM_ID_HERE`

## How It Works

1. When a user visits an album link:
   - If the app is installed: iOS automatically opens the app (universal link)
   - If not installed: User sees landing page with:
     - Album invitation message
     - Copy link button
     - Download on App Store button
     - Apple Smart App Banner

2. Smart redirect (optional):
   - Page attempts to open the app automatically
   - Falls back to landing page after 800ms if app doesn't open

3. After installation:
   - User can tap "Open" to return to the same album link
   - Or use the copied link to join the album