# GitHub Pages Deployment Guide

This guide will help you deploy your portfolio website to GitHub Pages using GitHub Actions.

## 📋 Prerequisites

- A GitHub account
- Git installed on your local machine
- Node.js 18+ installed
- Your project code ready

## 🚀 Deployment Steps

### Step 1: Create GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** icon in the top-right corner
3. Select **New repository**
4. Name your repository (e.g., `portfolio`)
5. Make sure **Public** is selected (required for free GitHub Pages)
6. Click **Create repository**

### Step 2: Configure Astro for GitHub Pages

Edit `astro.config.mjs` to match your repository:

```javascript
// @ts-check
import { defineConfig } from 'astro/config';
import tailwind from '@astrojs/tailwind';

export default defineConfig({
    // CASE 1: If your repository is: username.github.io
    site: 'https://<your-username>.github.io',
    // Remove the 'base' line for CASE 1
    
    // CASE 2: If your repository is: username.github.io/portfolio
    site: 'https://<your-username>.github.io/portfolio',
    base: '/portfolio',
    
    integrations: [tailwind()],
});
```

#### Understanding site and base:

- **If deploying to `username.github.io` (user/organization pages)**
  - `site`: `https://username.github.io`
  - `base`: (don't include this line)
  - URL will be: `https://username.github.io`

- **If deploying to `username.github.io/repo-name` (project pages)**
  - `site`: `https://username.github.io/repo-name`
  - `base`: `/repo-name`
  - URL will be: `https://username.github.io/repo-name`

Replace `<your-username>` with your actual GitHub username and `repo-name` with your repository name.

### Step 3: Initialize Git and Push

From your project directory:

```bash
# Initialize git if not already done
git init

# Add all files
git add .

# Make initial commit
git commit -m "Initial commit: Portfolio with Aceternity UI"

# Rename main branch (if needed)
git branch -M main

# Add remote repository
# Replace <username> and <repo-name> with your values
git remote add origin https://github.com/<username>/<repo-name>.git

# Push to GitHub
git push -u origin main
```

### Step 4: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click on **Settings** tab
3. In the left sidebar, click on **Pages**
4. Under **Build and deployment**, click **Configure**
5. For **Source**, select **GitHub Actions**
6. Click **Save**

### Step 5: Deploy

The GitHub Actions workflow will automatically:

1. Trigger when you push to `main` branch
2. Install dependencies
3. Build the Astro site
4. Deploy to GitHub Pages

You can watch the progress:

1. Go to your repository
2. Click on **Actions** tab
3. Select the **Deploy to GitHub Pages** workflow
4. Click on the latest run to see the progress

### Step 6: Access Your Site

After a few minutes, your site will be live at:

- **User pages**: `https://username.github.io`
- **Project pages**: `https://username.github.io/repo-name`

## 🔄 Making Updates

To update your site:

```bash
# Make changes to your code

# Stage changes
git add .

# Commit changes
git commit -m "Your commit message"

# Push to GitHub
git push origin main
```

The workflow will automatically deploy your changes!

## 📊 Workflow Details

### What the Workflow Does

The `.github/workflows/deploy.yml` file automates:

1. **Triggers**: On push to `main` branch or manual trigger
2. **Setup**: Checks out code, sets up Node.js 20
3. **Install**: Runs `npm ci` for clean installation
4. **Build**: Runs `npm run build` to generate static files
5. **Upload**: Uploads the `dist` folder as an artifact
6. **Deploy**: Deploys to GitHub Pages

### Workflow Permissions

The workflow requires these permissions (already set in the file):

```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```

## 🔧 Troubleshooting

### Images not loading after deployment

If images are broken after deploying to GitHub Pages with a `base` path:

**Solution**: Use `import.meta.env.BASE_URL` for all image paths in Astro components.

```astro
<!-- ❌ Wrong (absolute path) -->
<img src="/avatar.png" alt="Avatar" />

<!-- ✅ Correct (uses BASE_URL) -->
<img src={import.meta.env.BASE_URL + "/avatar.png"} alt="Avatar" />
```

This is already configured in:
- `src/pages/index.astro` - Avatar image
- `src/layouts/BaseLayout.astro` - Favicon and OG image

### Site not loading after deployment

1. **Wait a few minutes** - GitHub Pages can take 1-5 minutes to deploy
2. **Check Actions tab** - Ensure the workflow completed successfully
3. **Check Pages settings** - Verify Source is set to "GitHub Actions"
4. **Clear browser cache** - Try accessing in incognito mode

### Build errors in Actions

1. Go to Actions tab and click on the failed workflow
2. Check the error logs
3. Common issues:
   - Missing dependencies → Run `npm install` locally and commit
   - TypeScript errors → Fix local errors before pushing
   - Build timeout → Check for large assets or slow operations

### 404 errors

1. **Check `base` configuration** in `astro.config.mjs`
2. Verify it matches your repository structure
3. For project pages, ensure `base` starts with `/`

### Wrong site URL

1. Verify `site` in `astro.config.mjs` matches your GitHub Pages URL
2. Check that the repository name is correct
3. Ensure the repository is public

### Workflow not triggering

1. Verify you're pushing to the `main` branch
2. Check that the workflow file is at `.github/workflows/deploy.yml`
3. Ensure your repository has Actions enabled

## 🎯 Best Practices

### Branch Management

- **Main branch**: Production (auto-deploys)
- **Feature branches**: For development (`git checkout -b feature-name`)
- **Pull requests**: Review before merging to main

```bash
# Create a feature branch
git checkout -b feature/new-component

# Make changes and commit
git add .
git commit -m "Add new component"

# Push feature branch
git push origin feature/new-component

# Create Pull Request on GitHub
# After review, merge to main
```

### Pre-deployment Testing

Always test locally before pushing:

```bash
# Build locally
npm run build

# Preview locally
npm run preview
```

Visit `http://localhost:4321` to verify.

### Custom Domain

To use a custom domain with GitHub Pages:

1. Go to **Settings** > **Pages**
2. Under **Custom domain**, add your domain (e.g., `yourdomain.com`)
3. Configure DNS settings:
   - Add `CNAME` record pointing to `username.github.io`
4. Create `public/CNAME` file with your domain:
   ```
   yourdomain.com
   ```

## 📝 Environment Variables

If you need environment variables:

1. Go to repository **Settings** > **Secrets and variables** > **Actions**
2. Click **New repository secret**
3. Add your variables

### Adding Environment Variables to Workflow

Edit `.github/workflows/deploy.yml`:

```yaml
env:
  BUILD_PATH: "."
  YOUR_VAR_NAME: ${{ secrets.YOUR_SECRET_NAME }}
```

## 🔐 Security Considerations

- **Never commit sensitive data** (API keys, passwords)
- Use GitHub Secrets for environment variables
- Keep dependencies updated: `npm audit fix`
- Enable branch protection rules for `main` branch

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Astro Deployment Guide](https://docs.astro.build/en/guides/deploy/github/)
- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)

## ✅ Deployment Checklist

Before deploying, ensure:

- [ ] Repository is public
- [ ] `astro.config.mjs` has correct `site` and `base` settings
- [ ] GitHub Actions workflow is enabled
- [ ] Build succeeds locally (`npm run build`)
- [ ] No sensitive data in code
- [ ] All links in the site work
- [ ] Site looks correct in both light and dark modes
- [ ] Mobile responsiveness is tested

---

Your portfolio is ready to deploy! 🚀