# School Finder HK - Progressive Web App

## Project Overview

School Finder HK is a Progressive Web Application (PWA) designed to browse and search Hong Kong school information. The application allows users to filter schools by name, district, and type, compare schools side-by-side, and install the app directly on Android and iOS devices.

**Course:** COMP 3130SEF Mobile Application Project

## Features

### Core Features
- **Search & Filter**: Find schools by name, district, and school type
- **School Comparison**: Compare up to 3 schools side-by-side with detailed information
- **Data Export**: Export selected schools in JSON format for further analysis
- **Online/Offline Support**: Works seamlessly online with automatic caching for offline access
- **Responsive Design**: Optimized for mobile devices (Android, iPhone) and desktop browsers

### PWA Capabilities
- **Installable**: Can be installed as a native-like app on Android and iOS
- **Offline Access**: Service Worker caches essential assets and previously loaded data
- **Fast Load Times**: Cached resources load instantly even on slow connections
- **Icon & Splash Screens**: Professional branding on mobile home screens
- **Network Status Detection**: Visual indicators for online/offline status

## Project Structure

```
PWA/
├── school-info-pwa.html       # Main application HTML/CSS/JavaScript
├── manifest.webmanifest       # PWA manifest for app installation
├── sw.js                       # Service Worker for offline caching
├── icon.svg                    # App icon (192x192 and 512x512)
├── requirement.txt             # Project requirements
└── README.md                   # This file
```

## Technical Stack

- **Frontend**: Vanilla HTML5, CSS3, JavaScript (ES6+)
- **PWA Technologies**: 
  - Web App Manifest
  - Service Worker API
  - Cache API
  - Fetch API
- **Data Source**: Hong Kong Education Bureau (EDB) School Location and Information API
- **Deployment**: Static hosting (any web server)

## API Information

### Primary Data Source
- **API**: Hong Kong EDB School Location and Information
- **URL**: `https://www.edb.gov.hk/attachment/en/student-parents/sch-info/sch-search/sch-location-info/SCH_LOC_EDB.json`
- **Reference**: [Data.gov.hk - School Location and Information](https://data.gov.hk/en-data/dataset/hk-edb-schinfo-school-location-and-information)

### Data Format
The API returns JSON with school records containing:
- School Name
- District
- School Type (Primary, Secondary, Kindergarten, International, etc.)
- Address
- Telephone
- Email
- Website
- Latitude/Longitude coordinates
- Remarks

### Fallback
Sample data is provided for demonstration if the API is unavailable.

## Installation & Deployment

### Prerequisites
- A modern web browser (Chrome, Firefox, Safari, Edge)
- HTTPS hosting (required for PWA on Android)
- Web server to serve static files

### Deployment Steps

1. **Copy files to web server**:
   ```
   - school-info-pwa.html
   - manifest.webmanifest
   - sw.js
   - icon.svg
   - README.md
   ```

2. **Configure HTTPS**:
   PWAs require HTTPS for security (except localhost)
   - Use Let's Encrypt for free SSL certificates
   - Configure your web server (Apache, Nginx, etc.)

3. **Serve with proper MIME types**:
   - `manifest.webmanifest`: `application/manifest+json`
   - `sw.js`: `application/javascript` or `text/javascript`

4. **Verify deployment**:
   - Open `https://your-domain.com/school-info-pwa.html`
   - Check browser DevTools → Application → Manifest
   - Verify Service Worker is registered

### CORS & Mixed Content Issues

If the API is blocked due to CORS:
1. Use the "Load sample data" button in the app
2. Or implement a CORS proxy server:
   ```
   https://cors.example.com/https://www.edb.gov.hk/...
   ```

## How to Use

### Desktop/Browser
1. Open the application in a web browser
2. Click "Load data" to fetch school information
3. Use filters to search for specific schools
4. Select schools to compare by clicking "Add compare"
5. View comparison table at the bottom
6. Click "Export compare list" to download selected schools as JSON

### Mobile Installation (Android)

1. **Open in Chrome or compatible browser**:
   - Navigate to the PWA URL
   - Wait for page to fully load

2. **Install as app**:
   - An "Install app" button appears after loading
   - Click the button and confirm installation
   - OR use Chrome menu → "Add to Home Screen"

3. **Launch app**:
   - Find "School Finder HK" icon on your home screen
   - Tap to launch in standalone mode

### iOS Installation

1. Open in Safari
2. Tap the Share button
3. Select "Add to Home Screen"
4. Name the app and add to home screen
5. Launch from home screen

## Features in Detail

### Search & Filter
- **Search by name**: Type school name to find matches
- **Filter by district**: Select a specific district
- **Filter by type**: Choose Primary, Secondary, International, or Kindergarten
- **Sort results**: Organize by name, district, or type
- **Quick filter chips**: Click category buttons to filter instantly

### Compare Schools
- **Add to comparison**: Click "Add compare" on any school card
- **Maximum 3 schools**: Compare feature supports up to 3 schools
- **Detailed comparison table**: View side-by-side information
- **Export data**: Download comparison as JSON for reports/analysis
- **Clear comparisons**: Reset the compare list

### Offline Features
- **Automatic caching**: All assets cached on first load
- **Offline indicator**: Green dot = online, Orange dot = offline
- **Data persistence**: Previously loaded school data available offline
- **Cache status**: Shows "Offline cache enabled" when ready

## Browser Support

| Browser | Desktop | Mobile | PWA |
|---------|---------|--------|-----|
| Chrome  | ✓       | ✓      | ✓   |
| Firefox | ✓       | ✓      | ✓   |
| Safari  | ✓       | ✓      | ✓ (iOS 15+) |
| Edge    | ✓       | ✓      | ✓   |

## Performance Metrics

- **Installable**: PWA meets installability criteria
- **HTTPS**: Required for security and PWA features
- **Offline-first**: Service Worker enables offline-first strategy
- **Progressive enhancement**: Works with or without JavaScript
- **Mobile optimized**: 100% responsive layout

## Development Notes

### Service Worker Strategy
- **Cache-first**: For static assets (HTML, CSS, JS, icons)
- **Network-first**: For API calls (school data)
- **Network fallback**: Graceful degradation if resources unavailable

### Data Normalization
The app normalizes school data from various API formats by:
- Mapping common field names
- Handling missing values
- Validating coordinates
- Cleaning and escaping HTML

### State Management
- in-memory storage for:
  - All schools (allSchools)
  - Filtered results (filteredSchools)
  - Comparison list (compare)
  - PWA installation prompt (deferredPrompt)

## Known Limitations

1. **API Rate Limiting**: EDB API may have rate limits
2. **CORS**: Cross-origin requests may be blocked by some networks
3. **Map Integration**: Google Maps links require internet connection
4. **Large Datasets**: First load with full dataset may take time

## Future Enhancements

- [ ] Geolocation-based school search
- [ ] School ratings & reviews system
- [ ] Advanced filtering (location radius, fees, facilities)
- [ ] Dark mode support
- [ ] Multi-language support (English/Chinese)
- [ ] Push notifications for school updates
- [ ] Integration with other education APIs
- [ ] Academic performance comparisons

## Troubleshooting

### "Install app" button doesn't appear
- Ensure HTTPS is being used
- Check manifest.webmanifest loads correctly
- Service Worker must be registered successfully
- Browser DevTools → Application → Manifest to diagnose

### API data won't load
- Check internet connection
- Verify API URL is accessible
- Look for CORS errors in browser console
- Try "Load sample data" button instead

### Service Worker not registering
- Check browser console for errors
- Verify `sw.js` file path is correct
- Ensure HTTPS (or localhost for development)
- Try hard refresh (Ctrl+Shift+R)

### Offline access not working
- Wait for service worker installation to complete
- Cache status should show "Offline cache enabled"
- Try accessing the same page after going offline
- Check browser cache settings aren't blocking storage

## Testing Recommendations

### Manual Testing
1. Test search and filter functions
2. Test comparison with different school combinations
3. Test install process on Android device
4. Test offline functionality
5. Test export feature and JSON validity

### Automated Testing
- Validate manifest.webmanifest format
- Verify service worker registration
- Test API response handling
- Check HTML validity and accessibility
- Validate responsive design across devices

## Deployment Checklist

- [ ] All files uploaded to web server
- [ ] HTTPS configured and working
- [ ] manifest.webmanifest accessible at correct path
- [ ] Service Worker (sw.js) registering successfully
- [ ] Icons displaying correctly
- [ ] API endpoint is accessible
- [ ] Cache headers configured appropriately
- [ ] CORS headers set if needed
- [ ] Mobile testing completed (Android Chrome, Safari)
- [ ] Offline functionality verified

## References

- [MDN: Progressive Web Apps](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)
- [Google Web Fundamentals: PWAs](https://web.dev/progressive-web-apps/)
- [W3C: Web App Manifest](https://www.w3.org/TR/appmanifest/)
- [MDN: Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
- [Hong Kong EDB Data](https://data.gov.hk/en-data/dataset/hk-edb-schinfo-school-location-and-information)

## Support & Contact

For issues or questions about this application:
1. Check the troubleshooting section above
2. Review browser console for error messages
3. Verify all files are correctly deployed
4. Test in different browsers
5. Check GitHub Issues if available

## License

This project was developed for educational purposes as part of COMP 3130SEF Mobile Application Project.

---

**Version**: 1.0  
**Last Updated**: April 2, 2026  
**Status**: Production Ready
