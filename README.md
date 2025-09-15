# Deploy Eleventy from GitHub
![deployment-logo](https://github.com/user-attachments/assets/2f9fd805-110b-40c9-b123-1e7ffa0d3331)

Automated deployment workflows for [Eleventy](https://11ty.dev) static sites using GitHub Actions. Deploy to GitHub Pages, FTP servers, or SSH servers with integrated release management and deployment tracking.

> **Note:** For **Netlify** or **Cloudflare Pages**, you don't need this repository! Both platforms integrate directly with GitHub and can automatically build and deploy your Eleventy site. See their documentation:
>
> - [Netlify GitHub Integration](https://docs.netlify.com/git/overview/)
> - [Cloudflare Pages GitHub Integration](https://developers.cloudflare.com/pages/get-started/git-integration/)

## 🚀 Deployment Options

- **GitHub Pages** - Free hosting with automatic SSL
- **SSH Server** - Deploy to your own server via SSH
- **FTP Server** - Deploy to traditional web hosting
- **Manual Releases** - Create tagged GitHub releases for version tracking

## 📁 Project Structure

```text
.github/
├── actions/                   # Reusable GitHub Actions
│   ├── build/                 # Build Eleventy site
│   ├── deploy-github-pages/   # Deploy to GitHub Pages
│   ├── deploy-ftp/           # Deploy via FTP
│   ├── deploy-ssh/           # Deploy via SSH
│   └── new-release/          # Create releases
└── workflows/
    ├── create-release.yml     # Manual release creation
    ├── test.yml              # Test builds on pull requests
    └── examples/              # Example deployment workflows
        ├── deploy-github-pages.yml
        ├── deploy-ftp.yml
        └── deploy-ssh.yml
```

## ⚡ Quick Start

1. **Use this template** or fork this repository
2. **Add your Eleventy project** files to the repository root
3. **Choose a deployment method** and copy the appropriate workflow file from `.github/workflows/examples/` to `.github/workflows/`:
   - `deploy-github-pages.yml` for GitHub Pages
   - `deploy-ssh.yml` for SSH deployment  
   - `deploy-ftp.yml` for FTP deployment

4. **Configure secrets and variables** (see Configuration below)
5. **Push to main branch** to trigger deployment

## ⚙️ Configuration

### GitHub Pages

**Setup:**

- Enable GitHub Pages in **Settings → Pages**
- Set source to "GitHub Actions"

**Optional Variables:**

- `BUILD_COMMAND` - Build command (default: `npm run build`)
- `PUBLISH_DIR` - Build output directory (default: `_site`)

### SSH Deployment

**Required Secrets:**

- `SSH_SERVER` - Server hostname (e.g., `example.com`)
- `SSH_USERNAME` - SSH username
- `SSH_PRIVATE_KEY` - SSH private key content

**Required Variables:**

- `SITE_URL` - Your website URL (e.g., `https://example.com`)
- `SSH_SERVER_DIR` - Deploy directory (e.g., `/var/www/html`)

**Optional Variables:**

- `BUILD_COMMAND` - Build command (default: `npm run build`)
- `PUBLISH_DIR` - Build output directory (default: `_site`)
- `SSH_PORT` - SSH port (default: `22`)
- `SSH_EXCLUDE` - Files to exclude (comma separated)

### FTP Deployment

**Required Secrets:**

- `FTP_SERVER` - FTP server hostname
- `FTP_USERNAME` - FTP username
- `FTP_PASSWORD` - FTP password

**Required Variables:**

- `SITE_URL` - Your website URL

**Optional Variables:**

- `BUILD_COMMAND` - Build command (default: `npm run build`)
- `PUBLISH_DIR` - Build output directory (default: `_site`)
- `FTP_SERVER_DIR` - Upload directory (default: `/`)

### Manual Releases

**Setup:**

- No additional setup required
- Manually trigger via **Actions → Create Release**

**Required Permissions:**

- Actions → General → Workflow permissions set to "Read and write permissions"

**Optional Variables:**

- `BUILD_COMMAND` - Build command (default: `npm run build`)
- `PUBLISH_DIR` - Build output directory (default: `_site`)

## 🔧 Features

- **Automated deployment** on push to main branch
- **Manual deployment** via GitHub Actions tab
- **Deployment tracking** with status updates
- **Environment management** for production deployments
- **Automatic releases** with version tagging
- **Build testing** on pull requests

## 📝 SSH Key Setup

1. Generate SSH key pair:

   ```bash
   ssh-keygen -t rsa -b 4096 -C "github-actions"
   ```

2. Add public key to server's `~/.ssh/authorized_keys`
3. Add private key content to `SSH_PRIVATE_KEY` secret

## 🎯 Workflow Triggers

- **Push to main** - Automatic deployment
- **Pull requests** - Build testing only
- **Manual dispatch** - Run workflows manually

All secrets and variables are configured in **Settings → Secrets and variables → Actions**.

---

This repository demonstrates modern DevOps practices for static site deployment with GitHub Actions.
