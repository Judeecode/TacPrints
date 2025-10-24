# Pre-Deployment Checklist for Vercel

## ✅ Fixed Issues (Already Done)

- [x] Fixed `.gitignore` merge conflicts
- [x] Optimized `vercel.json` configuration
- [x] Created `.vercelignore` file
- [x] Verified asset paths are correct

## ⚠️ Critical Issues (YOU MUST FIX)

- [ ] **Replace or optimize `logo.svg` (989 KB → should be < 200 KB)**
- [ ] **Replace or optimize `footer-logo.svg` (843 KB → should be < 200 KB)**
- [ ] **Optimize or externally host `hero-vid.mp4` (2.04 MB → should be < 1 MB or external)**

## 📋 Pre-Deployment Checks

### 1. File Size Check
Run these commands to verify file sizes:

```bash
# Check logo size (should be < 200KB after optimization)
ls -lh assets/images/logo.*

# Check footer logo size (should be < 200KB after optimization)
ls -lh assets/images/footer-logo.*

# Check video size (should be < 1MB after optimization)
ls -lh assets/videos/hero-vid.mp4
```

### 2. Git Status Check
```bash
# Make sure all files are committed
git status

# Should show: "nothing to commit, working tree clean"
```

### 3. File Path Check
Verify these files exist:
- [ ] `assets/images/logo.png` (or optimized .svg)
- [ ] `assets/images/footer-logo.png` (or optimized .svg)
- [ ] `assets/videos/hero-vid.mp4` (or external URL)

### 4. HTML Reference Check
Verify `index.html` references match your files:
- [ ] Line 212: `<img src="assets/images/logo.___"`
- [ ] Line 902: `<img src="assets/images/footer-logo.___"`
- [ ] Line 228: `<source src="assets/videos/hero-vid.mp4"`

### 5. Vercel Configuration Check
- [x] `vercel.json` exists and is valid JSON
- [x] No PHP references in `vercel.json`
- [x] `.vercelignore` exists

### 6. Browser Test (Local)
Before deploying, test locally:
```bash
# Option 1: Using Python
python -m http.server 8000

# Option 2: Using Node.js
npx serve .

# Then open: http://localhost:8000
```

Check:
- [ ] Logo loads in navbar
- [ ] Footer logo loads
- [ ] Hero video plays
- [ ] No console errors (F12 → Console)

## 🚀 Ready to Deploy?

If all checks pass:

```bash
# 1. Stage all changes
git add .

# 2. Commit with descriptive message
git commit -m "Fix Vercel deployment: optimize media files and config"

# 3. Push to GitHub
git push origin main

# 4. Deploy to Vercel
# - Go to https://vercel.com
# - Import your repository
# - Click "Deploy"
```

## 🔍 Post-Deployment Verification

After deployment, check:

1. **Visit your Vercel URL**
2. **Open DevTools (F12) → Network tab**
3. **Verify these load successfully:**
   - [ ] `logo.png` (or .svg) - Status: 200
   - [ ] `footer-logo.png` (or .svg) - Status: 200
   - [ ] `hero-vid.mp4` - Status: 200
4. **Check Console tab** - Should have no errors
5. **Test on mobile** - Responsive design works

## ❌ If Images Still Don't Show

### Check 1: File Paths (Case Sensitive!)
Vercel uses Linux servers which are case-sensitive:
- ✅ Correct: `assets/images/logo.png`
- ❌ Wrong: `Assets/Images/Logo.png`
- ❌ Wrong: `assets/Images/logo.png`

### Check 2: Files Committed to Git
```bash
# List all files in assets/images
git ls-files assets/images/

# Should show your image files
```

### Check 3: Not in .gitignore
Make sure your images aren't being ignored:
```bash
# Check if file is ignored
git check-ignore assets/images/logo.png

# If it returns the file path, it's being ignored (BAD!)
# If it returns nothing, it's not ignored (GOOD!)
```

### Check 4: Vercel Build Logs
1. Go to https://vercel.com
2. Click your project
3. Click "Deployments"
4. Click latest deployment
5. Check "Build Logs" for errors

### Check 5: Browser Cache
Clear browser cache or test in incognito mode

## 🆘 Still Having Issues?

1. **Check Vercel deployment logs** for specific errors
2. **Verify file sizes** - Files > 5MB may fail
3. **Test locally first** - If it doesn't work locally, it won't work on Vercel
4. **Check browser console** - Look for 404 or CORS errors
5. **Verify Git repository** - Make sure all files are pushed

## 📊 Expected File Sizes After Optimization

| File | Current Size | Target Size | Status |
|------|-------------|-------------|--------|
| logo.svg | 989 KB | < 200 KB | ⚠️ TOO LARGE |
| footer-logo.svg | 843 KB | < 200 KB | ⚠️ TOO LARGE |
| hero-vid.mp4 | 2.04 MB | < 1 MB or external | ⚠️ TOO LARGE |

## 🎯 Success Criteria

Your deployment is successful when:
- ✅ Logo appears in navbar
- ✅ Footer logo appears
- ✅ Hero video plays automatically
- ✅ No 404 errors in console
- ✅ Page loads in < 3 seconds
- ✅ Works on mobile devices

---

**Remember:** The main issue is your SVG files have embedded 1MB PNG images. Fix this first!
