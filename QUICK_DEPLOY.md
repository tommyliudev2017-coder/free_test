# ⚡ Quick Deployment Reference

## 🎯 Fastest Way: Railway (Recommended)

### Step-by-Step (5 minutes):

1. **Sign up:** https://railway.app → Login with GitHub

2. **Create Project:**
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your repository

3. **Add Database (if needed):**
   - Click "+ New" → "Database" → "Add MySQL"
   - Railway auto-creates connection variables

4. **Set Environment Variables:**
   ```
   APP_ENV=production
   APP_DEBUG=false
   APP_KEY=base64:YOUR_KEY_HERE
   ```
   (Get APP_KEY by running `php artisan key:generate` locally)

5. **Deploy:**
   - Railway auto-detects Laravel and deploys
   - Wait 2-3 minutes
   - Your app is live! 🎉

---

## 🔑 Required Environment Variables

**Minimum Required:**
```
APP_ENV=production
APP_DEBUG=false
APP_KEY=base64:...
APP_URL=https://your-app.railway.app
```

**If using Database:**
```
DB_CONNECTION=mysql
DB_HOST=...
DB_DATABASE=...
DB_USERNAME=...
DB_PASSWORD=...
```

**Get APP_KEY:**
```bash
php artisan key:generate
# Copy the key from .env file
```

---

## 🚀 One-Time Setup Commands

Run these BEFORE first deployment:

```bash
# 1. Generate app key
php artisan key:generate

# 2. Build assets
npm install
npm run build

# 3. Test locally
php artisan serve
```

---

## 📦 What Gets Deployed

✅ **Included:**
- All PHP files
- `composer.json` (dependencies auto-installed)
- `package.json` (assets need building)
- Database migrations
- Configuration files

❌ **NOT Included (in .gitignore):**
- `.env` file (set via platform)
- `vendor/` (auto-installed)
- `node_modules/` (auto-installed)
- Storage files

---

## 🎯 Platform Comparison

| Feature | Railway | Render | Fly.io |
|---------|---------|--------|--------|
| **Free Tier** | $5 credit/month | 750 hrs/month | 3 VMs |
| **Sleeps?** | ❌ No | ✅ Yes (15min) | ❌ No |
| **Database** | ✅ Free MySQL | ✅ Free PostgreSQL | ❌ Paid |
| **Ease** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Best For** | Production | Testing/Dev | Advanced |

---

## ⚠️ Common Mistakes to Avoid

1. ❌ **Don't commit `.env`** - Already in .gitignore ✅
2. ❌ **Don't forget `APP_KEY`** - Required for encryption
3. ❌ **Don't set `APP_DEBUG=true`** in production
4. ❌ **Don't forget to build assets** - Run `npm run build`
5. ❌ **Don't use SQLite in production** - Use MySQL/PostgreSQL

---

## 🔧 Quick Fixes

**App shows 500 error:**
```bash
# On Railway/Render dashboard:
# Set APP_DEBUG=true temporarily
# Check logs for error
# Fix issue
# Set APP_DEBUG=false
```

**Assets not loading:**
```bash
# Build assets locally:
npm run build

# Commit and push:
git add public/build
git commit -m "Build assets"
git push
```

**Database connection fails:**
- Check database credentials in environment variables
- Verify database is running
- Check firewall/network settings

---

## 📞 Need Help?

- **Railway:** https://docs.railway.app
- **Render:** https://render.com/docs
- **Laravel:** https://laravel.com/docs

---

## ✅ Pre-Flight Checklist

Before deploying, ensure:
- [ ] Code is committed to GitHub
- [ ] `.env` is NOT committed (check .gitignore)
- [ ] `APP_KEY` is generated
- [ ] Assets are built (`npm run build`)
- [ ] No `dd()` or debug code
- [ ] Database is set up (if needed)
- [ ] Environment variables are ready

**Ready? Deploy now! 🚀**
