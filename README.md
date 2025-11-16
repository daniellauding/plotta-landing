# 🚀 Plotta Landing Page

Minimalistic landing page for Plotta

## 🌐 Live Site

- **Landing Page**: https://app.plotta.io
- **Web App**: https://www.plotta.io

## 📁 What's This?

Simple, fast, and beautiful landing page for Plotta with:
- Feature showcase
- Download links for all platforms
- Direct link to web app
- Mobile responsive
- Dark theme
- Zero dependencies (pure HTML/CSS/JS)

## 🚀 Quick Deploy to Netlify

### Option 1: Via Netlify UI (Easiest)

1. **Push to GitHub**
   ```bash
   cd /Users/daniellauding/Work/instinctly/internal/plotta-landing
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/daniellauding/plotta-landing.git
   git push -u origin main
   ```

2. **Connect to Netlify**
   - Go to [netlify.com](https://netlify.com)
   - Click "Add new site" → "Import an existing project"
   - Choose GitHub → Select `plotta-landing` repo
   - Build settings:
     - **Build command**: (leave empty)
     - **Publish directory**: `.` (root directory)
   - Click "Deploy site"

3. **Add Custom Domain**
   - In Netlify dashboard, go to **Site settings** → **Domain management**
   - Click "Add custom domain"
   - Enter: `app.plotta.io`
   - Follow DNS instructions below

### Option 2: Via Netlify CLI (Faster)

```bash
cd /Users/daniellauding/Work/instinctly/internal/plotta-landing

# Install Netlify CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy
netlify deploy --prod

# When prompted:
# - Choose "Create & configure a new site"
# - Publish directory: . (current directory)
```

## 🌍 Domain Setup

You have two domains to set up:

1. **www.plotta.io** → Main web app (already deployed)
2. **app.plotta.io** → Landing page (new)

### DNS Configuration

Go to your domain registrar (where you bought plotta.io) and add these DNS records:

#### For app.plotta.io (Landing Page)

**Option A: If using Netlify DNS**
```
Type: CNAME
Name: app
Value: your-site-name.netlify.app
```

**Option B: If using external DNS (Cloudflare, Namecheap, etc.)**
1. In Netlify, go to Site settings → Domain management → app.plotta.io
2. You'll see a CNAME or A record value
3. Add that to your DNS provider:
   ```
   Type: CNAME
   Name: app
   Value: [value from Netlify]
   ```

#### Current Setup (Don't Change!)

Keep these as they are:

```
# Main web app
Type: CNAME
Name: www
Value: [your current deployment]

# Root domain redirect
Type: A
Name: @
Value: [current value]
```

### SSL Certificate

Netlify automatically provisions SSL certificates. After adding the custom domain:
1. Wait 5-10 minutes
2. Netlify will verify domain ownership
3. SSL certificate auto-issued
4. HTTPS will work automatically

## 📝 File Structure

```
plotta-landing/
├── index.html          # Landing page (single file!)
├── favicon.svg         # Logo/favicon (optional)
└── README.md           # This file
```

## 🎨 Customization

### Update Download Links

When you have actual release URLs, edit `index.html`:

```javascript
// Around line 350
document.getElementById('download-mac').addEventListener('click', (e) => {
    e.preventDefault();
    // Replace with:
    window.location.href = 'https://github.com/daniellauding/plotta-desktop/releases/latest/download/Plotta-mac.dmg';
});

document.getElementById('download-windows').addEventListener('click', (e) => {
    e.preventDefault();
    // Replace with:
    window.location.href = 'https://github.com/daniellauding/plotta-desktop/releases/latest/download/Plotta-win.exe';
});
```

### Update Colors

In `index.html`, find the `:root` CSS variables:

```css
:root {
    --bg: #0a0a0a;        /* Background */
    --fg: #ededed;        /* Foreground text */
    --accent: #3b82f6;    /* Accent color (blue) */
    --muted: #737373;     /* Muted text */
    --border: #262626;    /* Borders */
}
```

### Add More Sections

Just add HTML before the `</main>` tag. It's a single file, so edit directly!

## 🚀 Deployment Checklist

- [ ] Push code to GitHub
- [ ] Deploy to Netlify
- [ ] Add custom domain `app.plotta.io`
- [ ] Update DNS records
- [ ] Wait for SSL (5-10 min)
- [ ] Test https://app.plotta.io
- [ ] Update download links when ready
- [ ] Add favicon.svg (optional)

## 🔄 Update Process

To update the landing page:

```bash
# 1. Make changes to index.html
# 2. Commit and push
git add .
git commit -m "Update landing page"
git push

# Netlify auto-deploys from main branch!
```

## 📊 Analytics (Optional)

Add Google Analytics or Plausible:

```html
<!-- Add before </head> in index.html -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_ID');
</script>
```

## 🎯 Current URLs Summary

After setup, you'll have:

| URL | Purpose | Deploys To |
|-----|---------|-----------|
| https://www.plotta.io | Main web app | Current deployment |
| https://app.plotta.io | Landing page | Netlify (this repo) |
| https://plotta.io | Redirects to www | DNS config |

## 🆘 Troubleshooting

### Domain not working?
- Wait 24-48 hours for DNS propagation
- Check DNS with: `dig app.plotta.io`
- Verify in Netlify: Domain settings → Check DNS configuration

### SSL not working?
- Wait 10 minutes after adding domain
- Netlify auto-renews SSL
- Check: Site settings → Domain management → HTTPS

### Changes not showing?
- Netlify auto-deploys from GitHub
- Check: Deploys tab in Netlify dashboard
- Clear browser cache (Cmd+Shift+R on Mac)

## 📞 Support

- Netlify docs: https://docs.netlify.com
- DNS help: https://docs.netlify.com/domains-https/custom-domains/
- Plotta issues: support@plotta.io

---

**Ready to deploy! 🎉**

Just run:
```bash
git push
netlify deploy --prod
```
