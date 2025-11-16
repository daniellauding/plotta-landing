# 🚀 Quick Setup Guide

## Step 1: Push to GitHub (2 minutes)

```bash
cd /Users/daniellauding/Work/instinctly/internal/plotta-landing

git init
git add .
git commit -m "Initial landing page"
git branch -M main
git remote add origin https://github.com/daniellauding/plotta-landing.git
git push -u origin main
```

## Step 2: Deploy to Netlify (3 minutes)

### Via Netlify Dashboard:

1. Go to https://app.netlify.com
2. Click "Add new site" → "Import an existing project"
3. Choose "GitHub"
4. Select `plotta-landing` repository
5. Settings:
   - **Build command**: (leave empty)
   - **Publish directory**: `.`
   - **Branch**: `main`
6. Click "Deploy site"
7. Wait 30 seconds for deployment

### Via Netlify CLI (Faster):

```bash
# Install CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy
netlify init

# Follow prompts:
# - Create & configure new site
# - Team: (your team)
# - Site name: plotta-landing
# - Publish directory: .

# Deploy
netlify deploy --prod
```

## Step 3: Add Custom Domain (2 minutes)

In Netlify dashboard:

1. Go to your site → **Site settings** → **Domain management**
2. Click "Add custom domain"
3. Enter: `app.plotta.io`
4. Click "Verify"

You'll see instructions like:
```
Add this DNS record:
Type: CNAME
Name: app
Value: your-site.netlify.app
```

## Step 4: Update DNS (5 minutes)

Go to where you manage DNS for `plotta.io` (Cloudflare, Namecheap, etc.):

### If using Cloudflare:

1. Log in to Cloudflare
2. Select `plotta.io` domain
3. Go to **DNS** → **Records**
4. Click "Add record"
5. Fill in:
   ```
   Type: CNAME
   Name: app
   Target: your-site.netlify.app
   Proxy status: DNS only (gray cloud)
   ```
6. Click "Save"

### If using Namecheap:

1. Log in to Namecheap
2. Go to Domain List → Manage → Advanced DNS
3. Click "Add New Record"
4. Fill in:
   ```
   Type: CNAME Record
   Host: app
   Value: your-site.netlify.app
   TTL: Automatic
   ```
5. Click "Save"

### If using other DNS provider:

Add a CNAME record:
- **Name/Host**: `app`
- **Value/Target**: `your-site.netlify.app` (from Netlify)
- **TTL**: 3600 or Auto

## Step 5: Wait for SSL (10 minutes)

Netlify automatically provisions SSL certificate:

1. In Netlify, go to **Domain settings** → **HTTPS**
2. You'll see "Waiting for DNS propagation"
3. Wait 5-15 minutes
4. When ready, it shows "✅ Your site has HTTPS enabled"

## Step 6: Test! (1 minute)

Open in browser:
- https://app.plotta.io (should load landing page)
- https://www.plotta.io (should load web app - already working)

## Summary of Domains

After setup:

| Domain | Points To | Purpose |
|--------|-----------|---------|
| **app.plotta.io** | Netlify (landing) | Landing page with downloads |
| **www.plotta.io** | Current deployment | Main web app |
| **plotta.io** | Redirect to www | Root domain |

## Verification

Check everything works:

```bash
# Test DNS
dig app.plotta.io

# Expected output:
# app.plotta.io.  300  IN  CNAME  your-site.netlify.app.

# Test SSL
curl -I https://app.plotta.io

# Expected:
# HTTP/2 200
# content-type: text/html
```

## Update Download Links Later

When you have macOS/Windows builds:

1. Create GitHub releases in `plotta-desktop` repo
2. Upload .dmg and .exe files
3. Edit `index.html` around line 350:

```javascript
document.getElementById('download-mac').href =
  'https://github.com/daniellauding/plotta-desktop/releases/latest/download/Plotta-mac.dmg';

document.getElementById('download-windows').href =
  'https://github.com/daniellauding/plotta-desktop/releases/latest/download/Plotta-win.exe';
```

4. Commit and push (auto-deploys!)

## Troubleshooting

### "Domain not found"
- DNS takes up to 24 hours to propagate
- Check with: `dig app.plotta.io`
- Make sure you added CNAME correctly

### "Not secure" warning
- Wait 10-15 minutes for SSL provisioning
- Check HTTPS settings in Netlify
- Try clearing browser cache

### Landing page not updating
- Check Deploys tab in Netlify
- Make sure you pushed to `main` branch
- Netlify auto-deploys on every push

### Need help?
- Netlify support: https://answers.netlify.com
- Email: support@plotta.io

---

## Done! 🎉

Your setup:
- ✅ Landing page at https://app.plotta.io
- ✅ Web app at https://www.plotta.io
- ✅ Auto-deploys on git push
- ✅ SSL enabled
- ✅ Mobile responsive

**Total time: ~15 minutes** (DNS propagation not included)
