# 🚀 GitHub Pages Hosting Guide

## How to Host MEP Sandbox Engine Website + Download on GitHub

Yes! You can host both the website AND the ZIP file on GitHub for free!

---

## 📋 Step-by-Step Setup

### 1. Create GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click **"New"** or **"+"** → **"New repository"**
3. Name it: `mep-sandbox-engine` (or any name you like)
4. Make it **Public**
5. Check **"Add a README file"**
6. Click **"Create repository"**

### 2. Upload Your Files

**Option A - Via Web Interface:**
1. Click **"Add file"** → **"Upload files"**
2. Drag these files from `DiscordEngVer/`:
   - `Mepsite.html`
   - `MicahEngineStudio_v1.1_Release.zip`
   - `MEPLua_Complete_Library_v1.1.md`
   - `README.md`
3. Click **"Commit changes"**

**Option B - Via Git (Advanced):**
```bash
cd DiscordEngVer
git init
git add .
git commit -m "Initial release v1.1"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/mep-sandbox-engine.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. In your repo, click **"Settings"**
2. Scroll to **"Pages"** in left sidebar
3. Under **"Source"**, select:
   - Branch: `main`
   - Folder: `/ (root)`
4. Click **"Save"**
5. Wait 1-2 minutes for deployment

### 4. Get Your Website URL

Your site will be live at:
```
https://YOUR_USERNAME.github.io/mep-sandbox-engine/Mepsite.html
```

Example:
```
https://micah-dev.github.io/mep-sandbox-engine/Mepsite.html
```

### 5. Update Download Link in Website

Now that your ZIP is on GitHub, update the download link:

**Edit `Mepsite.html` line ~830:**

Change:
```html
<a href="MicahEngineStudio_v1.1_Release.zip" class="btn" download>
```

To:
```html
<a href="https://github.com/YOUR_USERNAME/mep-sandbox-engine/raw/main/MicahEngineStudio_v1.1_Release.zip" class="btn" download>
```

**Example:**
```html
<a href="https://github.com/micah-dev/mep-sandbox-engine/raw/main/MicahEngineStudio_v1.1_Release.zip" class="btn" download>
```

**Important:** Use `/raw/main/` to get the direct download link!

### 6. Commit the Change

1. Click on `Mepsite.html` in GitHub
2. Click the pencil icon (Edit)
3. Update the download link
4. Click **"Commit changes"**
5. Wait 1-2 minutes for GitHub Pages to rebuild

---

## 🎯 Final Result

### Your Live Website:
```
https://YOUR_USERNAME.github.io/mep-sandbox-engine/Mepsite.html
```

### What Users Get:
- ✅ Beautiful modern website
- ✅ Complete MEPLua documentation
- ✅ Direct download link to ZIP (18.1 MB)
- ✅ Discord link to your community
- ✅ No ads, no paywalls, 100% free!

---

## 📢 Share Your Links

### On Discord:
```
🎮 **MEP Sandbox Engine v1.1**

🌐 Website: https://YOUR_USERNAME.github.io/mep-sandbox-engine/Mepsite.html
📥 Direct Download: https://github.com/YOUR_USERNAME/mep-sandbox-engine/raw/main/MicahEngineStudio_v1.1_Release.zip
💬 Discord: https://discord.gg/BsUQUFYBmN

Create 3D games with a Roblox-style editor!
```

### On Twitter/Social Media:
```
🎮 Released MEP Sandbox Engine v1.1!

A FREE Roblox-style game engine with MEPLua scripting.

🌐 Try it: [your-github-pages-link]
💬 Join: https://discord.gg/BsUQUFYBmN

#gamedev #indiedev #gameengine
```

---

## 📦 GitHub Release (Optional but Recommended)

Make it even easier for users:

1. In your repo, click **"Releases"** on right sidebar
2. Click **"Create a new release"**
3. Tag: `v1.1.0`
4. Title: `MEP Sandbox Engine v1.1`
5. Description:
```markdown
## MEP Sandbox Engine v1.1

Professional Roblox-inspired game development platform.

### Features
- 50+ object types
- MEPLua scripting
- Transform gizmos
- Multi-selection & grouping
- Character rigging tools

### Installation
1. Download the ZIP below
2. Extract to any folder
3. Run MicahEngineStudio.exe
4. Start creating!

### Links
- 🌐 Documentation: https://YOUR_USERNAME.github.io/mep-sandbox-engine/Mepsite.html
- 💬 Discord: https://discord.gg/BsUQUFYBmN

No Python or dependencies required!
```

6. Click **"Choose a file"** and upload `MicahEngineStudio_v1.1_Release.zip`
7. Click **"Publish release"**

Now users can download from:
```
https://github.com/YOUR_USERNAME/mep-sandbox-engine/releases/download/v1.1.0/MicahEngineStudio_v1.1_Release.zip
```

---

## 🎨 Custom Domain (Optional)

Want a custom URL like `mepsandbox.com`?

1. Buy domain from Namecheap, GoDaddy, etc. (~$10/year)
2. In GitHub Pages settings, add custom domain
3. Update DNS records (GitHub provides instructions)
4. Your site becomes: `https://mepsandbox.com`

---

## 📊 GitHub Pages Limits

✅ **FREE with no limits for:**
- Static HTML/CSS/JS
- Files up to 100 MB each
- Total repo size up to 1 GB
- Unlimited bandwidth

✅ **Your ZIP (18.1 MB) is well within limits!**

---

## 🔄 How to Update

When you release v1.2:

1. Upload new ZIP to GitHub
2. Update `Mepsite.html` with new version info
3. Create new GitHub Release
4. Changes appear automatically!

---

## 🛠️ Advanced: Rename Homepage

Make `Mepsite.html` the default page:

**Option 1 - Rename File:**
```
Mepsite.html → index.html
```
Then URL becomes:
```
https://YOUR_USERNAME.github.io/mep-sandbox-engine/
```

**Option 2 - Add index.html redirect:**
Create `index.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="refresh" content="0; url=Mepsite.html">
</head>
</html>
```

---

## ✅ Checklist

Before going live:

- [ ] Upload all files to GitHub
- [ ] Enable GitHub Pages
- [ ] Update download link in Mepsite.html to GitHub raw URL
- [ ] Test website loads properly
- [ ] Test download link works
- [ ] Test Discord link works
- [ ] Share links on Discord!

---

## 🎉 You're Live!

Your engine is now available worldwide for FREE!

Users can:
- Browse docs on your website
- Download directly from GitHub
- Join your Discord community
- Share with friends

**No hosting costs, no bandwidth limits, no ads!**

---

## 📧 Need Help?

If you run into issues:
1. Check GitHub Pages docs: https://pages.github.com
2. Ask in Discord: https://discord.gg/BsUQUFYBmN
3. GitHub community forums

---

**Happy hosting! 🚀**
