# Deployment Guide for Job Portal

This guide covers how to deploy your Job Portal application to different platforms.

## Prerequisites

1. Build the React app:
   ```bash
   cd client
   npm install
   npm run build
   ```

2. Install server dependencies:
   ```bash
   cd server
   pip install -r requirements.txt
   ```

## Platform-Specific Configurations

### 1. Netlify
- Use the `netlify.toml` file in the root directory
- Or manually configure:
  - Build command: `cd client && npm run build`
  - Publish directory: `client/dist`
  - Add `_redirects` file in `client/` directory

### 2. Vercel
- Use the `vercel.json` file in the root directory
- Or manually configure:
  - Build command: `cd client && npm run build`
  - Output directory: `client/dist`

### 3. Traditional Web Server (Apache)
- Upload the contents of `client/dist/` to your web server
- Ensure the `.htaccess` file is included for proper routing

### 4. Nginx
- Use the configuration in `nginx.conf.example`
- Upload the contents of `client/dist/` to your web server

### 5. Full Stack Deployment (Flask + React)

#### Option A: Single Server
1. Build the React app: `npm run build`
2. Start the Flask server: `python server/run.py`
3. Flask will serve both API and static files

#### Option B: Separate Deployment
1. Deploy React app to static hosting (Netlify/Vercel)
2. Deploy Flask API to Python hosting (Heroku/Railway/etc.)
3. Update the API URL in `client/src/config.ts`

## Environment Variables

Make sure to set these environment variables for production:

### Server (.env file):
```
SECRET_KEY=your-production-secret-key
DATABASE_URL=your-production-database-url
JWT_SECRET_KEY=your-jwt-secret-key
EMAIL_USER=your-email
EMAIL_PASS=your-email-password
```

### Client:
Update `client/src/config.ts` with your production API URL.

## Common Issues

### 1. 404 on Page Refresh
**Problem**: Direct navigation to routes like `/jobs` or `/login` returns 404.
**Solution**: Ensure your server/hosting platform is configured to serve `index.html` for all non-API routes.

### 2. API Calls Failing
**Problem**: Frontend can't connect to backend.
**Solution**: 
- Check CORS configuration
- Verify API URL in `config.ts`
- Ensure backend is running and accessible

### 3. Static Assets Not Loading
**Problem**: CSS/JS files return 404.
**Solution**: 
- Verify build output in `client/dist/`
- Check server static file serving configuration
- Ensure correct paths in HTML

## Testing Deployment

1. Build the app: `npm run build`
2. Start the server: `cd server && python run.py`
3. Visit: `http://localhost:5000`
4. Test navigation: `/`, `/jobs`, `/login`, `/register`
5. Test refresh on different routes
6. Test API functionality

## Security Checklist

- [ ] Change default secret keys
- [ ] Use HTTPS in production
- [ ] Configure proper CORS origins
- [ ] Validate all user inputs
- [ ] Use environment variables for sensitive data
- [ ] Enable database connection pooling
- [ ] Set up proper logging
