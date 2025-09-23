---
title: 👥 Team Collaboration Guide
description: How to edit and contribute to the UAGC DX Documentation
sidebar_position: 2
---

# 👥 Team Collaboration Guide

Welcome to the UAGC DX Documentation collaboration workflow! This guide shows you how to easily edit and contribute to our documentation using our enhanced GitHub-based system.

## 🚀 Quick Start: Editing Documentation

### Method 1: "Edit this Page" Links (Recommended)
**✨ Perfect for quick edits and content updates**

1. **📄 Find the page** you want to edit on the [documentation site](https://omac049.github.io/uagc-dx-documentation/)
2. **✏️ Click "Edit this page"** link at the bottom of any page
3. **🔧 Make your changes** directly in GitHub's web editor
4. **💾 Commit changes** with a descriptive message
5. **🚀 Auto-deploys** within 2-5 minutes!

:::tip Pro Tip
For small changes (typos, content updates, links), you can commit directly to main. For larger changes, create a pull request for review.
:::

### Method 2: GitHub Repository Editing
**🔧 For more complex edits or multiple files**

1. **🌐 Go to**: [GitHub Repository](https://github.com/omac049/uagc-dx-documentation)
2. **📁 Navigate to**: `new-docs/` folder  
3. **✏️ Click the pencil icon** (✏️) on any `.md` file
4. **🔧 Make your changes** 
5. **📝 Commit** or **create pull request**

## 📋 Documentation Standards

### ✍️ Writing Guidelines
- **Format**: Use Markdown with Docusaurus extensions
- **Style**: Follow existing patterns and tone
- **Links**: Use relative links for internal pages (`/getting-started`)
- **Images**: Store in `static/img/` directory
- **Code**: Use syntax highlighting with language specifications

### 📝 Content Structure
```markdown
---
title: Your Page Title
description: Brief description for SEO
sidebar_position: 1
---

# Your Page Title

Brief introduction paragraph.

## Main Section

Content here...

:::tip Helpful Tip
Use callouts for important information!
:::
```

### 🎨 Available Callouts
```markdown
:::tip Success
For positive outcomes and helpful tips
:::

:::warning Important
For important information that needs attention
:::

:::danger Critical
For critical warnings or breaking changes
:::

:::info Note
For general information and context
:::
```

## 🔄 Team Workflow Options

### Option A: Direct Editing (Simple)
**👥 Best for**: Content updates, fixes, small changes

```
See issue → Click "Edit this page" → Make changes → Commit → ✅ Live in 2-5 minutes
```

### Option B: Pull Request Workflow (Recommended)
**👥 Best for**: New sections, major changes, team review

```
Create branch → Make changes → Submit PR → Review → Merge → ✅ Live
```

## 🤖 What Happens Automatically

### ✅ When You Make Changes:
- **🔍 Automatic validation** of your changes
- **🏗️ Build testing** to ensure nothing breaks  
- **🛡️ Security scanning** for dependencies
- **🔗 Link checking** to prevent broken links
- **📊 Performance monitoring** of build times
- **🚀 Automatic deployment** to the live site

### ✅ When You Create a Pull Request:
- **🧪 Comprehensive testing** of your changes
- **📝 Automatic preview builds** 
- **💬 Status updates** posted as comments
- **📋 Detailed validation reports**
- **🏷️ Automatic labeling** and categorization

### ✅ Weekly Maintenance:
- **🔄 Automated dependency updates** every Monday
- **🛡️ Security patches** applied automatically  
- **📝 Auto-generated pull requests** for updates
- **🧪 Full testing** before any updates go live

## 👨‍💻 For Technical Team Members

### Local Development Setup
```bash
# One-time setup
git clone https://github.com/omac049/uagc-dx-documentation.git
cd DX-Documentation-New
npm install

# For each editing session  
npm start  # Live preview at localhost:3000
# Edit files in new-docs/ folder
# Commit and push changes
```

### Advanced Workflow Commands
```bash
# Test your changes locally
npm run build          # Build production version
npm run serve          # Serve built version locally

# Documentation maintenance  
npm run updates         # Generate recent updates page
npm run check-dates     # Validate all timestamps
npm run docs-health     # Full documentation health check
```

## 🆘 Getting Help & Support

### 📚 Quick Reference
- **Documentation Issues**: Create issue in GitHub repository
- **Urgent Content**: Use direct editing for immediate fixes
- **Major Changes**: Use pull request workflow for review
- **Technical Problems**: Contact development team

### 🔧 Common Tasks
| Task | How To | Time to Live |
|------|--------|--------------|
| Fix typo | Edit this page → Commit | 2-5 minutes |
| Update content | Edit this page → Commit | 2-5 minutes |
| Add new page | Create new .md file | 2-5 minutes |
| Major restructure | Pull request workflow | After review |

### 🚨 Troubleshooting
**❓ "Edit this page" not working?**
- Check if you have repository access
- Try refreshing the page
- Contact admin for permissions

**❓ Changes not appearing?**
- Wait 2-5 minutes for deployment
- Check GitHub Actions for build status
- Clear browser cache

**❓ Build failing?**
- Check GitHub Actions logs
- Verify markdown syntax
- Ask development team for help

## 🎯 Best Practices

### ✅ Do's
- **📝 Write clear commit messages** describing what you changed
- **🔍 Preview your changes** before committing (if editing locally)
- **📱 Consider mobile users** when formatting content
- **🔗 Test internal links** after making changes
- **📋 Follow existing content patterns** and structure

### ❌ Don'ts  
- **🚫 Don't commit broken markdown** - it will fail the build
- **🚫 Don't delete critical files** without team discussion
- **🚫 Don't make major structural changes** without review
- **🚫 Don't forget to update navigation** when adding new sections

## 📊 Success Metrics

**Our Goal**: ↘ time-to-answer, ↘ QA slips, ↘ Slack back-and-forth; ↗ first-call resolution.

### 🎯 How This Workflow Helps:
- **⚡ Faster updates** - Documentation stays current with minimal effort
- **👥 Team ownership** - Everyone can contribute directly
- **🔒 Quality assurance** - Automated testing prevents issues
- **📈 Better coverage** - Easier contribution = more comprehensive docs

---

## 🎉 Ready to Contribute?

Your documentation contribution workflow is now **enterprise-grade** and **team-friendly**! 

**Next Steps:**
1. **🧪 Try it out** - Find a page and click "Edit this page"
2. **📝 Make a small change** - Fix a typo or update content  
3. **⏱️ Watch it deploy** - See your changes live in minutes
4. **🎯 Share with team** - Help others discover how easy it is

**Questions?** Drop a message in Slack or create an issue in the GitHub repository!

:::tip 🚀 Pro Tip
Bookmark this guide and share it with new team members. The easier we make documentation updates, the better our team knowledge becomes!
:::
