# PREFICTION Frontend

B2B SaaS Marketing Website - Static Frontend

## Quick Start

### Local Development
```bash
# Using Python (no dependencies needed)
python -m http.server 3001

# Visit: http://localhost:3001
```

Or use any HTTP server:
```bash
# Node.js
npx http-server -p 3001

# NPM
npm start
```

## Structure

- `index.html` - Main landing page
- `admin.html` - Admin submissions panel
- `script.js` - Frontend logic & routing
- `style.css` - Custom styling
- `assets/` - Images and media

## Features

- ✅ Landing page with services & audiences
- ✅ Dynamic page routing (no backend required for navigation)
- ✅ Contact form (posts to backend API)
- ✅ Admin panel (requires backend)
- ✅ Responsive design
- ✅ Tailwind CSS styling

## API Integration

Frontend communicates with backend API:

```javascript
// Default: http://localhost:3000
// Can be configured via window.PREFICTION_API_BASE
```

### API Endpoints Used:
- `POST /api/contact` - Submit contact form
- `GET /admin/submissions` - Get submissions (requires auth)
- `POST /admin/verify` - Verify admin password
- `POST /admin/logout` - Logout admin session

## Deployment

### Option 1: Vercel (Recommended)
```bash
vercel deploy
```

### Option 2: Netlify
```bash
netlify deploy --prod --dir=.
```

### Option 3: GitHub Pages
Push to gh-pages branch or use GitHub Actions

### Option 4: Any Static Host
Upload to AWS S3, Firebase Hosting, Azure Static Web Apps, etc.

## Configuration

Set custom API base before loading script:
```html
<script>
  window.PREFICTION_API_BASE = 'https://api.yourdomain.com';
</script>
<script src="script.js"></script>
```

## Performance

- Static site (no build step)
- Tailwind CSS via CDN
- ~100KB total JS (script.js)
- Lazy loading for images
- Optimized for Core Web Vitals

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers

## Troubleshooting

**Admin panel shows 404?**
- Ensure backend is running
- Check API base URL configuration

**Contact form not submitting?**
- Verify backend is accessible
- Check browser console for errors
- Ensure MONGODB_URI is set on backend

**Images not loading?**
- Check assets/ folder exists
- Verify file names match script.js references
- Check deployment path configuration

## Next Steps

1. Deploy backend separately (see `/backend/README.md`)
2. Configure API_BASE to point to backend
3. Deploy frontend to CDN/static host
4. Test form submission end-to-end

---

**Ready to deploy?** See backend README for server deployment instructions.
