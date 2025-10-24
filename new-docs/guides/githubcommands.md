---
is_guide: true
owner: Development Team
last_updated: 2025-10-24
difficulty: Beginner
description: "A comprehensive guide to essential GitHub features and commands for managing the UAGC website repository, including cloning, branching, committing, pull requests, and more."
related_guides:
  - title: Development Workflows
    url: ../development-workflows/
  - title: Release & Incident Management
    url: ./release-incident/
  - title: QA Smoke Test
    url: ./qa-smoke-test/
---

# GitHub Commands & Features Guide

This guide provides a comprehensive overview of essential GitHub features and commands for managing the UAGC website repository.

## Cloning a Repository

1. **Step 1**: Navigate to the repository on GitHub (e.g., `https://github.com/uagc/uagc.edu`)
2. **Step 2**: Click the green "Code" button
3. **Step 3**: Copy the repository URL
4. **Step 4**: Open your terminal and run:
   ```bash
   git clone https://github.com/uagc/uagc.edu.git
   ```
5. **Step 5**: Navigate into the cloned directory:
   ```bash
   cd uagc.edu
   ```

## Creating a New Branch

1. **Step 1**: Ensure you're on the main branch:
   ```bash
   git checkout main
   ```
2. **Step 2**: Pull the latest changes:
   ```bash
   git pull origin main
   ```
3. **Step 3**: Create and switch to a new branch:
   ```bash
   git checkout -b feature/new-landing-page
   ```
4. **Step 4**: Verify you're on the new branch:
   ```bash
   git branch
   ```

## Making and Committing Changes

1. **Step 1**: Make your code changes in your editor
2. **Step 2**: Check which files have been modified:
   ```bash
   git status
   ```
3. **Step 3**: Stage the files you want to commit:
   ```bash
   git add path/to/file.html
   # Or stage all changes:
   git add .
   ```
4. **Step 4**: Commit your changes with a descriptive message:
   ```bash
   git commit -m "Add new landing page for uagc.edu/online-programs"
   ```
5. **Step 5**: Push your changes to the remote repository:
   ```bash
   git push origin feature/new-landing-page
   ```

## Creating a Pull Request

1. **Step 1**: Push your branch to GitHub (if not already done)
2. **Step 2**: Navigate to the repository at `https://github.com/uagc/uagc.edu`
3. **Step 3**: Click "Pull requests" tab, then "New pull request"
4. **Step 4**: Select your branch to compare with main
5. **Step 5**: Add a title and description explaining your changes
6. **Step 6**: Request reviews from team members
7. **Step 7**: Click "Create pull request"

## Reviewing and Merging Pull Requests

1. **Step 1**: Navigate to the pull request on GitHub
2. **Step 2**: Review the "Files changed" tab to see all modifications
3. **Step 3**: Add comments or request changes if needed
4. **Step 4**: Approve the pull request when ready
5. **Step 5**: Click "Merge pull request" button
6. **Step 6**: Confirm the merge and delete the branch if no longer needed

## Syncing Your Local Branch

1. **Step 1**: Switch to your main branch:
   ```bash
   git checkout main
   ```
2. **Step 2**: Fetch all remote changes:
   ```bash
   git fetch origin
   ```
3. **Step 3**: Pull and merge remote changes:
   ```bash
   git pull origin main
   ```
4. **Step 4**: Update your feature branch with latest main:
   ```bash
   git checkout feature/new-landing-page
   git merge main
   ```

## Resolving Merge Conflicts

1. **Step 1**: Identify conflicted files:
   ```bash
   git status
   ```
2. **Step 2**: Open conflicted files in your editor
3. **Step 3**: Look for conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
4. **Step 4**: Manually edit the file to resolve conflicts
5. **Step 5**: Stage the resolved files:
   ```bash
   git add path/to/resolved-file.html
   ```
6. **Step 6**: Complete the merge:
   ```bash
   git commit -m "Resolve merge conflicts for uagc.edu homepage"
   ```

## Viewing Commit History

1. **Step 1**: View complete commit history:
   ```bash
   git log
   ```
2. **Step 2**: View condensed one-line history:
   ```bash
   git log --oneline
   ```
3. **Step 3**: View history for a specific file:
   ```bash
   git log -- path/to/file.html
   ```
4. **Step 4**: View changes in a specific commit:
   ```bash
   git show [commit-hash]
   ```

## Reverting Changes

1. **Step 1**: Discard unstaged changes to a file:
   ```bash
   git checkout -- path/to/file.html
   ```
2. **Step 2**: Unstage a staged file:
   ```bash
   git reset path/to/file.html
   ```
3. **Step 3**: Revert a specific commit (creates new commit):
   ```bash
   git revert [commit-hash]
   ```
4. **Step 4**: Reset to a previous commit (use with caution):
   ```bash
   git reset --hard [commit-hash]
   ```

## Working with Remote Repositories

1. **Step 1**: View configured remotes:
   ```bash
   git remote -v
   ```
2. **Step 2**: Add a new remote:
   ```bash
   git remote add upstream https://github.com/uagc/uagc.edu.git
   ```
3. **Step 3**: Fetch from a specific remote:
   ```bash
   git fetch upstream
   ```
4. **Step 4**: Remove a remote:
   ```bash
   git remote remove upstream
   ```

## Using Git Stash

1. **Step 1**: Save uncommitted changes temporarily:
   ```bash
   git stash
   ```
2. **Step 2**: List all stashes:
   ```bash
   git stash list
   ```
3. **Step 3**: Apply the most recent stash:
   ```bash
   git stash apply
   ```
4. **Step 4**: Apply and remove the most recent stash:
   ```bash
   git stash pop
   ```
5. **Step 5**: Delete all stashes:
   ```bash
   git stash clear
   ```

## Tagging Releases

1. **Step 1**: Create a lightweight tag:
   ```bash
   git tag v1.0.0
   ```
2. **Step 2**: Create an annotated tag with message:
   ```bash
   git tag -a v1.0.0 -m "Release version 1.0.0 for uagc.edu"
   ```
3. **Step 3**: Push tags to remote:
   ```bash
   git push origin --tags
   ```
4. **Step 4**: View all tags:
   ```bash
   git tag -l
   ```

## Best Practices

- Write clear, descriptive commit messages that explain the "why" not just the "what"
- Create feature branches for all new work; never commit directly to main
- Pull the latest changes from main before starting new work
- Keep commits small and focused on a single purpose
- Review your own code before requesting reviews from others
- Delete merged branches to keep the repository clean
- Use meaningful branch names (e.g., `feature/`, `bugfix/`, `hotfix/`)
- Always test your changes locally before pushing
- Document any special setup or configuration in commit messages
- Communicate with your team about major changes or refactors

## Common Workflow Example

Here's a typical workflow for updating a page on uagc.edu:

```bash
# 1. Start from main branch
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b update/about-page-content

# 3. Make your changes to the about page
# Edit files in your editor...

# 4. Stage and commit changes
git add about.html
git commit -m "Update about page content and images for uagc.edu/about"

# 5. Push to GitHub
git push origin update/about-page-content

# 6. Create pull request on GitHub
# Navigate to https://github.com/uagc/uagc.edu and create PR

# 7. After merge, clean up
git checkout main
git pull origin main
git branch -d update/about-page-content
```

## Related Resources

- [Development Workflows](../development-workflows.md)
- [Release & Incident Management](release-incident.md)
- [QA Smoke Test](qa-smoke-test.md)
- [Content Updates Guide](../content-updates.md)
