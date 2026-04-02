# GitHub Pages Deployment Guide

## Repository Information
- **Repository**: cyril15532/MobileAPP
- **Live URL**: https://cyril15532.github.io/MobileAPP/
- **Branch**: main (or your default branch)

## Steps to Deploy on GitHub Pages

### 1. Initialize Git Repository
```bash
cd c:\Users\User\Downloads\PWA
git init
git add .
git commit -m "Initial PWA commit"
```

### 2. Add Remote Repository
```bash
git remote add origin https://github.com/cyril15532/MobileAPP.git
git branch -M main
git push -u origin main
```

### 3. Enable GitHub Pages
1. Go to https://github.com/cyril15532/MobileAPP/settings
2. Navigate to **Pages** section (left sidebar)
3. Under "Source", select **main** branch
4. Under folder, select **/ (root)**
5. Click **Save**

### 4. Wait for Deployment
- GitHub will build and deploy your site automatically
- Initial deployment takes 1-2 minutes
- Access the app at: https://cyril15532.github.io/MobileAPP/

## File Structure for GitHub Pages
```
MobileAPP/
├── .nojekyll                   # Disables Jekyll processing
├── manifest.webmanifest        # PWA manifest
├── school-info-pwa.html        # Main app
├── sw.js                        # Service Worker
├── icon.svg                     # App icon
├── README.md                    # Documentation
└── GITHUB_PAGES_SETUP.md        # This file
```

## Important Notes

### HTTPS is Automatic
- GitHub Pages automatically uses HTTPS
- PWA features will work out of the box
- Icons will display correctly on home screens

### Path Configuration
- All paths in configuration files are set for GitHub Pages subdirectory
- `start_url` in manifest: `/MobileAPP/school-info-pwa.html`
- Service Worker scope: `/MobileAPP/`
- Change `MobileAPP` to your actual repository name if different

### Installation on Mobile

**Android (Chrome)**:
1. Visit: https://cyril15532.github.io/MobileAPP/
2. Wait for page to fully load
3. Click the "Install app" button (appears after loading)
4. Confirm installation
5. App appears on home screen

**iOS (Safari)**:
1. Visit: https://cyril15532.github.io/MobileAPP/
2. Tap Share button → Add to Home Screen
3. Name the app and add to home screen
4. Launch from home screen

## Custom Domain (Optional)

If you want to use a custom domain instead of github.io:

1. Update `CNAME` file in repository root:
   ```
   your-domain.com
   ```

2. Update paths in configuration files:
   - `manifest.webmanifest`: Change `start_url` to `/school-info-pwa.html` (remove MobileAPP)
   - `school-info-pwa.html`: Update service worker scope to `/`
   - `sw.js`: Update BASE_PATH to `/`

3. Configure DNS records at your domain registrar:
   - Add CNAME pointing to `cyril15532.github.io`

## Troubleshooting GitHub Pages

### Site Not Loading
- Verify repository is public (Settings → Visibility)
- Check GitHub Pages is enabled in Settings
- Clear browser cache (Ctrl+Shift+Delete)
- Wait 5 minutes for deployment to complete

### Install Button Not Appearing
- Ensure HTTPS URL is used (https://, not http://)
- Verify manifest.webmanifest loads (DevTools → Network)
- Check service worker registers (DevTools → Application → Service Workers)

### PWA Not Installing
- Must use HTTPS (GitHub Pages provides this automatically)
- Wait for service worker to fully register
- Try with Chrome or Edge on Android
- Check DevTools Console for errors

### Service Worker Issues
- GitHub Pages may cache files for 5 minutes
- Force refresh (Ctrl+Shift+R) to bypass cache
- Clear browser cache and site data
- Check .nojekyll file exists in repository

## Testing Before Deploy

### Local Testing with HTTPS
```bash
# Using Python 3
python -m http.server 8000

# Then access: http://localhost:8000/school-info-pwa.html
```

Note: PWA features require HTTPS except on localhost

### Verification Checklist
- [ ] All files pushed to GitHub
- [ ] GitHub Pages enabled in Settings
- [ ] Site accessible at https://cyril15532.github.io/MobileAPP/
- [ ] Manifest loads without errors
- [ ] Service Worker registers
- [ ] Install button appears on mobile
- [ ] Can load sample data
- [ ] Offline mode works
- [ ] Comparison feature works

## Performance Optimization (Optional)

### Enable GitHub Pages Caching
Create `.gitattributes` file:
```
* text=auto
*.js text eol=lf
*.html text eol=lf
*.css text eol=lf
*.svg text eol=lf
*.json text eol=lf
```

### Minimize Bundle
- All assets are already minimal
- No npm packages required
- No build process needed

## CI/CD with GitHub Actions (Optional)

Create `.github/workflows/pages.yml` for automated deployment:
```yaml
name: Build and Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
```

## Support

For GitHub Pages specific issues:
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [GitHub Pages Troubleshooting](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages)

For PWA issues on GitHub Pages:
- Check manifest.webmanifest loads correctly
- Verify .nojekyll file blocks Jekyll processing
- Ensure HTTPS is used (automatic on GitHub Pages)
- Check browser DevTools for console errors

---

**Last Updated**: April 2, 2026
