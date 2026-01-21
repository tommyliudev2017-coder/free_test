# 🚀 Laravel Deployment Guide - Free Hosting Options

## ✅ Pre-Deployment Fixes Applied
- ✅ Removed `dd()` debug statements from production code
- ✅ Added missing `Log` facade imports
- ✅ Code is now production-ready

---

## 🎯 Recommended Free Hosting Services

### 1. **Railway** (⭐ BEST CHOICE)
**Why Choose Railway:**
- ✅ $5/month free credit (usually enough for small apps)
- ✅ Easy GitHub integration
- ✅ Auto HTTPS
- ✅ Supports PHP 8.2 & Laravel 12
- ✅ Free MySQL/PostgreSQL
- ✅ No sleep/restrictions

**Deployment Steps:**
1. Sign up at https://railway.app (use GitHub)
2. Click "New Project" → "Deploy from GitHub repo"
3. Select your repository
4. Railway auto-detects Laravel
5. Add MySQL database (if needed)
6. Set environment variables (see below)
7. Deploy!

**Environment Variables Needed:**
```
APP_NAME=YourAppName
APP_ENV=production
APP_KEY=base64:YOUR_KEY_HERE
APP_DEBUG=false
APP_URL=https://your-app.railway.app

DB_CONNECTION=mysql
DB_HOST=your-db-host
DB_PORT=3306
DB_DATABASE=your-database
DB_USERNAME=your-username
DB_PASSWORD=your-password

# Mail settings (use Mailtrap or similar for testing)
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=your-username
MAIL_PASSWORD=your-password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@yourdomain.com
```

---

### 2. **Render** (Good Alternative)
**Why Choose Render:**
- ✅ 750 free hours/month
- ✅ Free PostgreSQL database
- ✅ Auto HTTPS
- ⚠️ Sleeps after 15 min inactivity (free tier)

**Deployment Steps:**
1. Sign up at https://render.com
2. Connect GitHub account
3. Click "New" → "Web Service"
4. Select your repository
5. Configure:
   - **Build Command:** `composer install --no-dev && php artisan migrate --force`
   - **Start Command:** `php artisan serve --host=0.0.0.0 --port=8000`
   - **Environment:** PHP
6. Add PostgreSQL database (free)
7. Set environment variables
8. Deploy!

**Note:** For production, use a process manager. Render provides one automatically.

---

### 3. **Fly.io** (More Control)
**Why Choose Fly.io:**
- ✅ 3 free VMs
- ✅ 3GB storage
- ✅ Good performance
- ⚠️ Requires more setup

**Deployment Steps:**
1. Install Fly CLI: `curl -L https://fly.io/install.sh | sh`
2. Sign up: `fly auth signup`
3. Initialize: `fly launch` (in your project directory)
4. Follow prompts
5. Deploy: `fly deploy`

---

## 📋 Pre-Deployment Checklist

### 1. **Environment Configuration**
Create `.env` file with production settings:
```bash
APP_ENV=production
APP_DEBUG=false
APP_URL=https://your-domain.com
```

### 2. **Generate Application Key**
```bash
php artisan key:generate
```

### 3. **Database Setup**
- If using SQLite: Ensure `database/database.sqlite` exists
- If using MySQL/PostgreSQL: Create database and update `.env`

### 4. **Run Migrations**
```bash
php artisan migrate --force
```

### 5. **Build Assets**
```bash
npm install
npm run build
```

### 6. **Optimize for Production**
```bash
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan optimize
```

### 7. **Storage Link**
```bash
php artisan storage:link
```

### 8. **Set Permissions** (if on Linux)
```bash
chmod -R 775 storage bootstrap/cache
chown -R www-data:www-data storage bootstrap/cache
```

---

## 🔧 Platform-Specific Configuration

### Railway Configuration
Create `railway.json` (optional):
```json
{
  "$schema": "https://railway.app/railway.schema.json",
  "build": {
    "builder": "NIXPACKS"
  },
  "deploy": {
    "startCommand": "php artisan serve --host=0.0.0.0 --port=$PORT",
    "restartPolicyType": "ON_FAILURE",
    "restartPolicyMaxRetries": 10
  }
}
```

### Render Configuration
Create `render.yaml`:
```yaml
services:
  - type: web
    name: laravel-app
    env: php
    buildCommand: composer install --no-dev && php artisan migrate --force && npm install && npm run build
    startCommand: php artisan serve --host=0.0.0.0 --port=8000
    envVars:
      - key: APP_ENV
        value: production
      - key: APP_DEBUG
        value: false
```

---

## 🗄️ Database Options

### Free Database Services:
1. **Railway MySQL** - Included with Railway
2. **Render PostgreSQL** - Free tier available
3. **Supabase** - Free PostgreSQL (https://supabase.com)
4. **PlanetScale** - Free MySQL (https://planetscale.com)

### Using Supabase (PostgreSQL):
1. Sign up at https://supabase.com
2. Create new project
3. Get connection string from Settings → Database
4. Update `.env`:
```
DB_CONNECTION=pgsql
DB_HOST=your-host.supabase.co
DB_PORT=5432
DB_DATABASE=postgres
DB_USERNAME=postgres
DB_PASSWORD=your-password
```

---

## 📧 Email Configuration (Free Options)

### Option 1: Mailtrap (Testing)
- Sign up: https://mailtrap.io
- Free tier: 500 emails/month
- Use for development/testing

### Option 2: SendGrid (Production)
- Sign up: https://sendgrid.com
- Free tier: 100 emails/day
- Good for production

### Option 3: Mailgun
- Free tier: 5,000 emails/month
- Requires credit card

---

## 🔒 Security Checklist

- ✅ Remove all `dd()`, `dump()`, `var_dump()` statements
- ✅ Set `APP_DEBUG=false` in production
- ✅ Use strong `APP_KEY`
- ✅ Use HTTPS (auto-enabled on Railway/Render)
- ✅ Set secure session/cookie settings
- ✅ Use environment variables for secrets
- ✅ Enable CSRF protection (already enabled)
- ✅ Validate all file uploads (already implemented)

---

## 🚨 Common Deployment Issues

### Issue: "500 Internal Server Error"
**Solution:**
- Check `APP_DEBUG=true` temporarily to see error
- Verify `.env` file exists and is configured
- Check `storage/` and `bootstrap/cache/` permissions
- Run `php artisan config:clear`

### Issue: "Class not found"
**Solution:**
- Run `composer install --no-dev`
- Run `php artisan optimize:clear`

### Issue: "Database connection failed"
**Solution:**
- Verify database credentials in `.env`
- Check if database is accessible from hosting IP
- Ensure database exists

### Issue: "Assets not loading"
**Solution:**
- Run `npm run build` before deployment
- Verify `public/build/` directory exists
- Check `vite.config.js` settings

---

## 📝 Post-Deployment Steps

1. **Test all functionality:**
   - User registration/login
   - Admin access
   - File uploads
   - PDF generation
   - Email sending

2. **Monitor logs:**
   ```bash
   # Railway
   railway logs
   
   # Render
   Check dashboard logs
   ```

3. **Set up backups:**
   - Database backups (if using external DB)
   - File storage backups

4. **Performance optimization:**
   - Enable OPcache
   - Use CDN for assets (optional)
   - Enable caching

---

## 🎉 Quick Start Commands

### For Railway:
```bash
# Install Railway CLI (optional)
npm i -g @railway/cli

# Login
railway login

# Link project
railway link

# Deploy
railway up
```

### For Render:
Just push to GitHub - auto-deploys!

---

## 💡 Pro Tips

1. **Use Git for version control** - All platforms support GitHub
2. **Set up staging environment** - Test before production
3. **Monitor resource usage** - Stay within free tier limits
4. **Use environment variables** - Never commit secrets
5. **Enable logging** - Monitor errors in production

---

## 📞 Need Help?

- **Railway Docs:** https://docs.railway.app
- **Render Docs:** https://render.com/docs
- **Fly.io Docs:** https://fly.io/docs
- **Laravel Docs:** https://laravel.com/docs

---

## ✅ Final Checklist Before Going Live

- [ ] All debug code removed
- [ ] `.env` configured for production
- [ ] Database migrations run
- [ ] Assets built (`npm run build`)
- [ ] Storage link created
- [ ] Email configured
- [ ] HTTPS enabled
- [ ] Error logging configured
- [ ] Admin account created
- [ ] Test all features

**Good luck with your deployment! 🚀**
