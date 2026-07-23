# Deploy to Vercel Guide

This guide will help you deploy your HR Job Application System to Vercel.

## Option 1: Deploy via Vercel CLI (Recommended)

### Prerequisites
- Node.js installed on your system
- Git installed on your system
- A Vercel account (free at https://vercel.com)

### Step 1: Install Vercel CLI
Open your terminal and run:
```bash
npm install -g vercel
```

### Step 2: Login to Vercel
```bash
vercel login
```
Follow the prompts to authenticate with your Vercel account.

### Step 3: Deploy
Navigate to your project directory:
```bash
cd "c:\Users\mckeo\Desktop\erp project"
```

Run the deployment command:
```bash
vercel
```

Follow the prompts:
- **Set up and deploy?** → Yes
- **Which scope?** → Select your account
- **Link to existing project?** → No
- **What's your project's name?** → hr-job-system (or any name you prefer)
- **In which directory is your code located?** → ./
- **Want to modify these settings?** → No

Vercel will deploy your application and provide a live URL (e.g., https://hr-job-system.vercel.app)

### Step 4: Deploy to Production
After testing the preview deployment, deploy to production:
```bash
vercel --prod
```

## Option 2: Deploy via Vercel Dashboard (No CLI)

### Step 1: Push to GitHub
1. Create a GitHub repository
2. Initialize git in your project:
```bash
cd "c:\Users\mckeo\Desktop\erp project"
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

### Step 2: Connect to Vercel
1. Go to https://vercel.com/dashboard
2. Click "Add New Project"
3. Import your GitHub repository
4. Click "Deploy"

Vercel will automatically detect the static HTML file and deploy it.

## Option 3: Drag and Drop (Simplest)

1. Go to https://vercel.com/new
2. Select "Upload a file or folder"
3. Drag and drop your `hr-system.html` file
4. Vercel will deploy it instantly

## After Deployment

Your application will be live at a URL like:
- https://hr-job-system.vercel.app
- https://your-project-name.vercel.app

### Important Notes:
- The Supabase credentials are already configured in the HTML file
- The application will work immediately after deployment
- No additional configuration needed
- The database is hosted on Supabase, so data persists across deployments

## Custom Domain (Optional)

If you want a custom domain:
1. Go to your Vercel project dashboard
2. Click "Settings" → "Domains"
3. Add your custom domain
4. Follow the DNS configuration instructions

## Troubleshooting

### Build Errors
If you encounter build errors, make sure:
- `vercel.json` is in the project root
- `hr-system.html` is in the project root

### Supabase Connection Issues
If the app can't connect to Supabase:
- Verify your Supabase project is active (not paused)
- Check that the credentials in `hr-system.html` are correct
- Ensure Row Level Security policies are set correctly

### 404 Errors
If you get 404 errors:
- Check the `routes` configuration in `vercel.json`
- Ensure the file path is correct

## Environment Variables (Optional)

If you want to use environment variables instead of hardcoded credentials:

1. In Vercel dashboard, go to Settings → Environment Variables
2. Add:
   - `NEXT_PUBLIC_SUPABASE_URL` = your Supabase URL
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY` = your Supabase anon key

2. Update `hr-system.html` to use:
```javascript
const SUPABASE_URL = process.env.NEXT_PUBLIC_SUPABASE_URL || 'YOUR_SUPABASE_URL_HERE';
const SUPABASE_ANON_KEY = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY || 'YOUR_SUPABASE_ANON_KEY_HERE';
```

Note: For static HTML files, environment variables require a build step. The current setup uses hardcoded credentials which work fine for this use case.
