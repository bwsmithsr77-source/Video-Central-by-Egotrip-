# GitHub Pages Deployment Configuration

This configuration enables automatic deployment of Video Central to GitHub Pages.

## Setup Steps

### 1. Enable GitHub Pages in Repository Settings

1. Go to **Settings** → **Pages**
2. Under "Source", select:
   - Branch: `main`
   - Folder: `/ (root)`
3. Click **Save**
4. Your site will be available at: `https://bwsmithsr77-source.github.io/Video-Central-by-Egotrip-`

### 2. Configure Custom Domain (Optional)

1. In **Settings** → **Pages**
2. Enter your custom domain (e.g., `video-central.example.com`)
3. Create DNS CNAME record pointing to `bwsmithsr77-source.github.io`
4. Verify domain in GitHub

### 3. This Repository Structure Supports GitHub Pages

The repository is already set up for GitHub Pages deployment:
- `index.html` is the main entry point (served as homepage)
- `video-central.html` is an alias/backup
- All files are in the root directory (easy deployment)
- No build step required (static HTML/CSS/JS)

## Deployment Flow

```
Push to main branch
        ↓
GitHub Pages rebuilds site
        ↓
Changes live at:
https://bwsmithsr77-source.github.io/Video-Central-by-Egotrip-
```

## Accessing Your App

### Direct Links

| Link | Purpose |
|------|---------|
| `https://bwsmithsr77-source.github.io/Video-Central-by-Egotrip-/` | Main app (index.html) |
| `https://bwsmithsr77-source.github.io/Video-Central-by-Egotrip-/index.html` | Explicit index |
| `https://bwsmithsr77-source.github.io/Video-Central-by-Egotrip-/video-central.html` | Alternate version |

### Testing Locally

```bash
# Start a local server
python3 -m http.server 8000

# Visit in browser
# http://localhost:8000/index.html
```

## Enabling HTTPS

GitHub Pages automatically provides HTTPS for all sites:
- ✅ Automatic HTTPS certificate
- ✅ Redirects HTTP to HTTPS
- ✅ Valid for all subdomains

## Adding a Custom Domain

If you own a domain:

1. **GitHub Settings**:
   - Go to **Settings** → **Pages**
   - Enter domain: `yoursite.com`

2. **DNS Provider** (e.g., GoDaddy, Namecheap):
   - Create CNAME record:
     ```
     Name: your-subdomain
     Type: CNAME
     Value: bwsmithsr77-source.github.io
     ```

3. **Verification**:
   - GitHub will verify the domain
   - Site available at `https://yoursite.com`

## Workflow Integration

### Automatic Deployment

Every push to `main` automatically triggers deployment:

```yaml
Push to main
    ↓
GitHub detects changes
    ↓
GitHub Pages rebuilds
    ↓
Site updated (within ~1-2 minutes)
```

### Manual Build (if needed)

```bash
git checkout main
git pull origin main
git push origin main  # Triggers GitHub Pages build
```

## Performance & Caching

- **Static Files**: Cached by GitHub CDN globally
- **Cache Bust**: Add query params `?v=1` for versioning
- **Build Time**: Usually 1-2 minutes
- **CDN**: Automatic global distribution

## Monitoring Deployment

1. Go to **Settings** → **Pages**
2. Look at "Deployments" section
3. View deployment status and history
4. Click on any deployment to see details

## Troubleshooting

### Site Not Updating

```bash
# Force a rebuild by making a commit
git commit --allow-empty -m "Trigger GitHub Pages build"
git push origin main
```

### HTTPS Issues

- Wait 24 hours for certificate to be issued
- Check if domain is correctly configured in DNS
- Clear browser cache

### File Not Found (404)

- Verify file exists in root directory
- Check file path is correct
- Ensure branches in Settings is pointing to `main`

## Disabling GitHub Pages

1. Go to **Settings** → **Pages**
2. Under "Source", select **None**
3. Click **Save**

## Features Now Available

✅ **Live Demo URL** - Share with users, no deployment needed  
✅ **No Server Cost** - GitHub Pages is free  
✅ **HTTPS by Default** - Secure connection  
✅ **Global CDN** - Fast access worldwide  
✅ **Auto-Deploy** - Push to main = live  
✅ **Version Control** - Full Git history  

## Next Steps

1. Push your changes to `main`
2. Wait 1-2 minutes for build
3. Visit your live URL
4. Share with users!

---

**Your Live App URL:**
```
https://bwsmithsr77-source.github.io/Video-Central-by-Egotrip-/
```

Test it now and share with your audience! 🚀
