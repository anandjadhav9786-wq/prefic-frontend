#  PREFICTION Frontend - Vercel Deployment Guide

## Overview

This is a static HTML/CSS/JS frontend for PREFICTION connected to your backend API running on Vercel.

**Backend**: https://prefic-backend-69r9.vercel.app
**Frontend** (to be deployed): Your new Vercel project

---

## Project Structure

\\\
frontend/
 index.html              # Main landing page
 admin.html              # Admin submissions dashboard
 script.js               # All JavaScript logic & API calls
 style.css               # All styling
 assets/                 # Images, logos, icons
 package.json            # Metadata (no npm dependencies)
 vercel.json             # Vercel configuration (static site)
 .env                    # Environment variables (API URL)
 .env.example            # Template for .env
 .gitignore              # Git exclusions
\\\

---

## Prerequisites

1.  Backend deployed: https://prefic-backend-69r9.vercel.app
2.  GitHub account
3.  Vercel account (free tier)

---

## Step 1: Create GitHub Repository for Frontend

### Option A: Using GitHub Web Interface

1. Go to: https://github.com/new
2. **Repository name**: prefic-frontend
3. **Description**: PREFICTION Frontend - B2B SaaS Marketing Website
4. **Public** (recommended for frontend)
5. Click "Create repository"

### Option B: Using Git CLI

\\\ash
cd C:\Users\anand\OneDrive\Desktop\frontend
git remote add origin https://github.com/anandjadhav9786-wq/prefic-frontend.git
git add .
git commit -m "Initial commit: PREFICTION frontend"
git branch -M main
git push -u origin main
\\\

---

## Step 2: Update Environment Variables

The frontend needs to know where the backend API is located.

### For Production (Vercel):

File: .env
\\\
PREFICTION_API_BASE=https://prefic-backend-69r9.vercel.app
NODE_ENV=production
\\\

### For Local Development:

File: .env
\\\
PREFICTION_API_BASE=http://localhost:3000
NODE_ENV=development
\\\

---

## Step 3: How the Frontend Connects to Backend

### In \script.js\:

\\\javascript
// Line ~303-307
const API_BASE = window.PREFICTION_API_BASE || (
  window.location.hostname === 'localhost'
    ? 'http://localhost:3000'
    : window.location.origin
);

// Contact form submission (Line ~343)
const res = await fetch(API_BASE + '/api/contact', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(formData)
});
\\\

### How it Works:

1. On page load, script.js checks for \window.PREFICTION_API_BASE\
2. If not set, it defaults to:
   - \http://localhost:3000\ if running locally
   - Current domain if in production
3. When user submits contact form, it POSTs to:
   - \{API_BASE}/api/contact\
   - Which resolves to: \https://prefic-backend-69r9.vercel.app/api/contact\

---

## Step 4: Deploy to Vercel

### Method 1: GitHub Integration (Recommended)

1. Go to: https://vercel.com/new
2. Click "Import from GitHub"
3. Select: \nandjadhav9786-wq/prefic-frontend\
4. **Configure Project**:
   - Framework Preset: **Other** (static site)
   - Root Directory: \./\
   - Build Command: Leave empty or \echo 'Static site'\
   - Output Directory: \./\
5. **Environment Variables**:
   - Add: \PREFICTION_API_BASE\ = \https://prefic-backend-69r9.vercel.app\
6. Click "Deploy"
7. Wait ~1-2 minutes for deployment

### Method 2: Vercel CLI

\\\ash
npm install -g vercel
vercel login
cd C:\Users\anand\OneDrive\Desktop\frontend
vercel --prod
\\\

---

## Step 5: Test the Deployment

### Health Check:
\\\ash
curl https://your-frontend-url/_health
# Note: Frontend doesn't have this, it will return 404
\\\

### Test Contact Form:
1. Visit your deployed frontend URL
2. Fill out the contact form
3. Submit
4. Check your backend admin panel:
   - https://prefic-backend-69r9.vercel.app/admin.html
   - Verify submission appears

### Test Admin Panel:
- https://your-frontend-url/admin.html
- Login with your ADMIN_PANEL_PASSWORD
- Manage submissions

---

## Post-Deployment Checklist

- [ ] Frontend deployed to Vercel
- [ ] Got Vercel URL (format: \https://prefic-frontend-xxx.vercel.app\  )
- [ ] Contact form submits successfully
- [ ] Submissions appear in backend admin panel
- [ ] Contact form shows success message
- [ ] All assets load (images, styles, scripts)
- [ ] Responsive design works on mobile
- [ ] Admin panel is accessible

---

## Troubleshooting

### Contact Form Not Submitting

**Problem**: Form submission fails or shows error

**Solutions**:
1. Check browser console (F12  Console tab)
2. Verify \PREFICTION_API_BASE\ is set correctly
3. Check backend is running: https://prefic-backend-69r9.vercel.app/api/status
4. Verify CORS is enabled (it is in backend)

### Admin Panel Not Loading

**Problem**: /admin.html shows 404

**Solutions**:
1. Check URL: \https://your-frontend-url/admin.html\
2. Verify admin.html exists in frontend folder
3. Clear browser cache and reload
4. Check Vercel deployment logs

### API Connection Error

**Problem**: "Unable to reach the API server"

**Solutions**:
1. Verify backend URL in .env: \https://prefic-backend-69r9.vercel.app\
2. Check backend status: https://prefic-backend-69r9.vercel.app/api/status
3. Verify MongoDB connection in backend
4. Add environment variable to Vercel project settings

---

## File Descriptions

| File | Purpose |
|------|---------|
| \index.html\ | Main landing page with all sections |
| \dmin.html\ | Admin dashboard (submissions list/delete) |
| \script.js\ | All JavaScript (animations, API calls, logic) |
| \style.css\ | All CSS styling |
| \ssets/\ | Images, logos, icons folder |
| \package.json\ | Project metadata (no npm packages needed) |
| \ercel.json\ | Vercel deployment config (static site) |
| \.env\ | Environment variables (not committed to git) |
| \.env.example\ | Template for .env |
| \.gitignore\ | Files to exclude from git |

---

## Environment Variables Reference

### PREFICTION_API_BASE

Controls where the frontend sends API requests.

**Values**:
- Development: \http://localhost:3000\
- Production: \https://prefic-backend-69r9.vercel.app\

**Used in**:
- Contact form submission
- Admin panel data fetching

### NODE_ENV

Controls runtime behavior.

**Values**:
- \development\: Enable debug logging
- \production\: Minimize logging

---

## API Endpoints Used by Frontend

| Endpoint | Method | Purpose |
|----------|--------|---------|
| \/api/contact\ | POST | Submit contact form |
| \/admin/submissions\ | GET/POST | Fetch submissions list |
| \/admin/submissions/:id\ | DELETE | Delete submission |
| \/admin/verify\ | POST | Admin login (password) |
| \/admin/logout\ | POST | Admin logout |

All requests go to: \{PREFICTION_API_BASE}{endpoint}\

---

## Development Tips

### Local Testing

\\\ash
# Set local backend URL
# In .env: PREFICTION_API_BASE=http://localhost:3000

# Start backend
cd C:\Users\anand\OneDrive\Desktop\backend
npm start

# Start frontend (Python http server)
cd C:\Users\anand\OneDrive\Desktop\frontend
python -m http.server 3001
# Visit: http://localhost:3001
\\\

### Update Backend URL (if needed)

If your backend URL changes, update in Vercel:
1. Go to project Settings  Environment Variables
2. Change \PREFICTION_API_BASE\
3. Redeploy

---

## Next Steps

1.  Push frontend to GitHub
2.  Deploy to Vercel
3.  Test contact form
4.  Verify admin panel
5.  Monitor submissions

Your frontend is now ready to work with your backend! 
