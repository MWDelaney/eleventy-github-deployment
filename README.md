# Deploy Eleventy from GitHub

This repository demonstrates how to deploy [Eleventy](https://11ty.dev) static sites to common hosting environments using GitHub Actions. It showcases automated deployment workflows with integrated release management and environment tracking.

## 🚀 Deployment Targets

This project includes workflows for deploying to:

- **GitHub Pages** - Built-in GitHub hosting with automatic SSL
- **FTP Server** - Traditional web hosting via FTP upload (not recommended, but included for completeness)
- **SSH Server** - Secure deployment via SSH
- **Manual Releases** - Create tagged releases without deployment

## 📁 Project Structure

```text
.github/
├── actions/
│   ├── build/                 # Reusable build action
│   ├── deploy-github-pages/   # GitHub Pages deployment action
│   ├── deploy-ftp/           # FTP deployment action
│   ├── deploy-ssh/           # SSH deployment action
│   └── new-release/          # Release creation action
└── workflows/
    ├── create-release.yml     # Manual release workflow
    └── examples/              # Example deployment workflows
        ├── deploy-github-pages.yml # GitHub Pages deployment workflow
        ├── deploy-ftp.yml         # FTP deployment workflow
        └── deploy-ssh.yml         # SSH deployment workflow
```

## 🔧 GitHub Integrations

### Releases

- **Automatic release creation** after successful deployments
- **Version tagging** based on commit SHA
- **Release notes** generated from commits
- **Artifact attachment** of built site files

### Deployments & Environments

- **Environment tracking** for production deployments
- **Deployment status** updates (pending, success, failure)
- **Environment URLs** automatically linked to deployment records
- **Deployment history** visible in repository insights

### Environment Configuration

Each deployment workflow creates and manages environments:

- **`github-pages`** - For GitHub Pages deployments (this is automatic from GitHub)
- **`production`** - For FTP and other production deployments

## ⚙️ Configuration

Configure your deployment target by setting up the appropriate secrets and variables in **Settings → Secrets and variables → Actions**.

### GitHub Pages Deployment

**Required Setup:**

- Enable GitHub Pages in **Settings → Pages**
- Configure source as "GitHub Actions"

**Variables (optional):**

- `BUILD_COMMAND` - Custom build command (defaults to `npm run build`)

### FTP Deployment

**Required Secrets (Settings → Secrets and variables → Actions → Secrets):**

- `FTP_SERVER` - Your FTP server hostname (e.g., `ftp.example.com`)
- `FTP_USERNAME` - Your FTP username
- `FTP_PASSWORD` - Your FTP password

**Required Variables (Settings → Secrets and variables → Actions → Variables):**

- `SITE_URL` - Your website URL (e.g., `https://example.com`)

**Optional Variables:**

- `BUILD_COMMAND` - Custom build command (defaults to `npm run build`)
- `FTP_SERVER_DIR` - FTP upload directory (defaults to `/`)

### SSH Deployment

**Required Secrets (Settings → Secrets and variables → Actions → Secrets):**

- `SSH_SERVER` - Your SSH server hostname (e.g., `example.com`)
- `SSH_USERNAME` - Your SSH username
- `SSH_PRIVATE_KEY` - Your SSH private key (the entire key contents)

**Required Variables (Settings → Secrets and variables → Actions → Variables):**

- `SITE_URL` - Your website URL (e.g., `https://example.com`)
- `SSH_SERVER_DIR` - Server directory to deploy to (e.g., `/var/www/html`)

**Optional Variables:**

- `BUILD_COMMAND` - Custom build command (defaults to `npm run build`)
- `SSH_PORT` - SSH port (defaults to `22`)
- `SSH_EXCLUDE` - Files to exclude from deployment (comma separated)

## 🔄 Workflow Triggers

### Automatic Deployment

All deployment workflows trigger on:

- **Push (or merge) to main branch** - Automatic production deployment
- **Manual dispatch** - Run workflow manually from Actions tab

## 📚 Getting Started

1. **Fork this repository** or use as template
2. **Configure your Eleventy project** in the repository root
3. **Choose your deployment method** and move the appropriate workflow:
   - For GitHub Pages: Move `.github/workflows/examples/deploy-github-pages.yml` to `.github/workflows/`
   - For FTP deployment: Move `.github/workflows/examples/deploy-ftp.yml` to `.github/workflows/`
   - For SSH deployment: Move `.github/workflows/examples/deploy-ssh.yml` to `.github/workflows/`
   - You can use multiple deployment methods by moving multiple files to the workflows directory
4. **Set up required secrets and variables** in repository settings (see Configuration section)
5. **Enable GitHub Pages** if using GitHub Pages deployment
6. **Push to main branch** to trigger first deployment

## 🔍 Monitoring Deployments

Track your deployments through:

- **Actions tab** - View workflow run details and logs
- **Environments** - See deployment history and status
- **Releases** - Browse tagged versions and artifacts
- **Deployments API** - Integrate with external monitoring tools

This project demonstrates modern DevOps practices for static site deployment, providing a foundation for production-ready Eleventy hosting workflows.
