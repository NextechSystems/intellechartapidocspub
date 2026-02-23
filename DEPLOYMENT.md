# Deployment Documentation

## Overview

This repository uses GitHub Actions for automated continuous deployment of the Nextech API documentation to GitHub Pages.

## Pipeline Location

The deployment pipeline is defined in `.github/workflows/deploy.yml`.

## How to Track Deployments

### 1. Check Deployment Status

**Via README Badges:**
- The README.md file displays status badges at the top showing the current build status
- Green badge = successful deployment
- Red badge = failed deployment

**Via GitHub Actions:**
- Visit the [Actions tab](https://github.com/NextechSystems/intellechartapidocspub/actions)
- Click on "Build and Deploy Documentation" workflow
- See all workflow runs with their status and details

### 2. Find the Latest Deployed Commit

**Method 1: Check gh-pages branch**
```bash
# View the latest deployment commit on gh-pages
git log gh-pages -n 1

# The commit message will show: "Deploy documentation from <source-commit-hash>"
```

**Method 2: Check GitHub Web Interface**
- Visit the [gh-pages branch commits](https://github.com/NextechSystems/intellechartapidocspub/commits/gh-pages)
- The latest commit message shows which source commit was deployed
- Example: "Deploy documentation from abc123..."

**Method 3: Check Workflow Runs**
- Visit [Workflow runs](https://github.com/NextechSystems/intellechartapidocspub/actions/workflows/deploy.yml)
- The most recent successful run shows what was deployed
- Click on a run to see the exact commit SHA that was deployed

### 3. Verify What's Live

The live documentation is available at: https://nextechsystems.github.io/intellechartapidocspub

To verify what's deployed:
1. Check the gh-pages branch for the latest commit
2. The commit message contains the source commit SHA
3. Compare with your local branch to see if your changes are live

## Deployment Process

### Automatic Deployment

The pipeline automatically runs when:
- Changes are pushed to the `master` branch
- A pull request is merged to `master`

The deployment process:
1. Checks out the repository
2. Sets up Ruby 3.3.7
3. Installs dependencies via Bundler
4. Builds the static site using Middleman
5. Deploys to the gh-pages branch
6. GitHub Pages automatically publishes the updated site

### Manual Deployment

You can manually trigger a deployment:
1. Go to [Actions tab](https://github.com/NextechSystems/intellechartapidocspub/actions/workflows/deploy.yml)
2. Click "Run workflow"
3. Select the branch (usually `master`)
4. Click "Run workflow" button

### Legacy Deployment Script

The `deploy.sh` script is still available for local deployments but is not recommended. Use the automated pipeline instead for better tracking and consistency.

## Troubleshooting

### Deployment Failed

If a deployment fails:
1. Check the [workflow run logs](https://github.com/NextechSystems/intellechartapidocspub/actions/workflows/deploy.yml)
2. Look for error messages in the build or deploy steps
3. Common issues:
   - Syntax errors in markdown files
   - Missing dependencies
   - Build failures in Middleman

### Changes Not Showing Up

If your changes aren't visible:
1. Verify the workflow completed successfully
2. Wait a few minutes for GitHub Pages to update (can take 5-10 minutes)
3. Clear your browser cache
4. Check that your changes were actually merged to master

## Monitoring

- **Workflow Status**: Check badges in README.md
- **Deployment History**: View commits on gh-pages branch
- **Build Logs**: Available in GitHub Actions for 90 days
- **Live Site**: https://nextechsystems.github.io/intellechartapidocspub
