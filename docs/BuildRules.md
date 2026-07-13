# Build Rules

Standards, procedures, and requirements for building, testing, releasing, and deploying the Gutter Cleaning & Repair website.

**Created:** 2026-07-13  
**Version:** 1.0  
**Status:** Framework established, implementation details pending Sprint 1

## Build Definition

A **build** is a complete, tested, documented version of the website ready for deployment or release.

### Build Components
- **Build Number:** Unique identifier (e.g., build-1.0.0)
- **Source Code:** All HTML, CSS, JavaScript, SVG files
- **Assets:** Images and other media
- **Documentation:** README, API docs, deployment guides
- **Changelog:** Summary of changes from previous build
- **Rollback Plan:** Procedure to revert if needed
- **Test Results:** Verification that build meets requirements

### Build Stages
1. **Development Build** → Internal testing only
2. **Preview Build** → Customer/stakeholder review
3. **Release Build** → Approved for production
4. **Production Build** → Live on production server

## Build Numbering

### Format: `MAJOR.MINOR.PATCH`

**MAJOR** — Breaking changes or major features
- Sprint 1 = 1.0.0
- Sprint 2 = 2.0.0
- New service offering = 2.0.0

**MINOR** — New features or improvements
- Sprint 1.1 = 1.1.0
- Sprint 1.2 = 1.2.0
- Bug fixes = 1.0.1 or 1.0.2

**PATCH** — Bug fixes and hotfixes
- Production hotfix = 1.0.1
- Critical issue fix = 1.0.2

### Build Tagging in Git
```
v1.0.0  → Sprint 1 Release
v1.0.1  → Sprint 1 Hotfix
v1.1.0  → Sprint 1.1 Release
v2.0.0  → Sprint 2 Release
```

## Development Build Procedure

### When Creating a Development Build

1. **Create Feature Branch**
   ```bash
   git checkout -b feature/descriptive-name
   ```

2. **Implement Changes**
   - Code new features
   - Fix identified issues
   - Update related documentation

3. **Self-Test**
   - Test in all target browsers
   - Verify responsive design
   - Check asset loading
   - Validate links and forms

4. **Local Build Verification**
   - All files present and correct
   - No broken links or missing assets
   - CSS styles applied correctly
   - JavaScript functionality working
   - SVG graphics rendering properly

5. **Prepare Commit**
   - Write clear commit message
   - Include what changed and why
   - Reference any related issues

### Commit Message Format
```
[FEATURE] Add responsive hero section

- Implemented mobile-optimized hero section
- Added background image optimization
- Updated CSS for all breakpoints
- Tested on devices from 320px - 1920px width

Related: Sprint-1, Build-1.0
```

## Preview Build Procedure

### When Moving to Preview for Review

1. **Create Preview Build**
   ```bash
   git checkout -b release/v1.0-preview
   ```

2. **Update Version**
   - Bump version number in package.json or config
   - Update in documentation
   - Note "Preview" status if applicable

3. **Build Documentation**
   - Update CHANGELOG.md
   - Document all changes from previous build
   - Note any breaking changes
   - Add deployment instructions

4. **Package for Preview**
   - Create `/previews/` build directory
   - Copy all production files
   - Include README with deployment steps
   - Include rollback procedure

5. **Preview Deployment**
   - Deploy to staging environment
   - Verify all features working
   - Test forms and interactions
   - Check performance metrics
   - Validate on multiple devices

6. **Preview Checkoff**
   - All features tested and working
   - Documentation complete and accurate
   - Performance acceptable
   - No critical issues identified
   - Stakeholder approval received (if required)

## Release Build Procedure

### When Ready for Production

1. **Create Release Branch**
   ```bash
   git checkout -b release/v1.0.0
   ```

2. **Final Version Updates**
   - Update all version numbers
   - Finalize CHANGELOG
   - Complete all documentation
   - Verify no uncommitted changes

3. **Release Testing**
   - Full functionality test
   - Cross-browser compatibility
   - Mobile responsiveness
   - Performance validation
   - Accessibility audit
   - SEO verification

4. **Create Release Package**
   ```
   /releases/v1.0.0/
   ├── index.html
   ├── /css/
   ├── /js/
   ├── /images/
   ├── /svg/
   ├── DEPLOYMENT.md
   ├── CHANGELOG.md
   ├── README.md
   └── ROLLBACK.md
   ```

5. **Merge to Main**
   ```bash
   git checkout main
   git merge --no-ff release/v1.0.0
   git tag -a v1.0.0 -m "Release version 1.0.0"
   git push origin main --tags
   ```

6. **Merge Back to Develop**
   ```bash
   git checkout develop
   git merge --no-ff release/v1.0.0
   git push origin develop
   ```

7. **Delete Release Branch**
   ```bash
   git branch -d release/v1.0.0
   ```

## Hotfix Procedure

### For Production Issues

1. **Create Hotfix Branch**
   ```bash
   git checkout -b hotfix/issue-description
   git checkout -b hotfix/critical-css-bug
   ```

2. **Implement Fix**
   - Make minimal changes to fix issue
   - Test thoroughly
   - Include test case if applicable

3. **Update Version**
   - Increment patch version: v1.0.0 → v1.0.1
   - Update CHANGELOG
   - Document fix clearly

4. **Merge to Main**
   ```bash
   git checkout main
   git merge --no-ff hotfix/critical-css-bug
   git tag -a v1.0.1 -m "Hotfix: critical CSS bug"
   git push origin main --tags
   ```

5. **Merge Back to Develop**
   ```bash
   git checkout develop
   git merge --no-ff hotfix/critical-css-bug
   git push origin develop
   ```

6. **Deploy Hotfix**
   - Deploy to production immediately
   - Verify fix is working
   - Monitor for related issues

## Testing Requirements

### Before Every Build

#### Functional Testing
- [ ] All pages load without errors
- [ ] All navigation links work
- [ ] Forms submit correctly (if applicable)
- [ ] All interactive elements respond to user input
- [ ] No console errors or warnings

#### Cross-Browser Testing
- [ ] Chrome/Edge (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Mobile Safari (iOS)
- [ ] Chrome (Android)

#### Responsive Design Testing
- [ ] Mobile (320px - 480px)
- [ ] Tablet (768px - 1024px)
- [ ] Desktop (1920px+)
- [ ] High-resolution displays
- [ ] Landscape and portrait orientations

#### Performance Testing
- [ ] Page load time < [target] seconds
- [ ] Time to interactive < [target] seconds
- [ ] No layout shifts (CLS < 0.1)
- [ ] Images optimized
- [ ] CSS/JS minified

#### Accessibility Testing
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Color contrast sufficient
- [ ] Focus indicators visible
- [ ] ARIA labels present where needed

#### SEO Verification
- [ ] Meta titles present and unique
- [ ] Meta descriptions filled
- [ ] Structured data valid
- [ ] Sitemap updated
- [ ] Robots.txt configured

## Deployment Checklist

### Before Deploying to Production

- [ ] All tests passing
- [ ] Documentation complete and accurate
- [ ] Rollback procedure documented
- [ ] Performance acceptable
- [ ] Security review completed
- [ ] Stakeholder approval received
- [ ] Backup of current production taken
- [ ] Monitoring alerts configured
- [ ] Team notified of deployment
- [ ] Rollback team on standby

### After Deployment

- [ ] Website loads in production
- [ ] All features working
- [ ] Performance meets targets
- [ ] Error logs reviewed
- [ ] Analytics updated
- [ ] Stakeholders notified

## Rollback Procedure

### Creating Rollback Point
Before major deployment:
```bash
git tag -a rollback-sprint-1 -m "Rollback point for Sprint 1"
git push origin rollback-sprint-1
```

### Executing Rollback
If critical issues occur:
```bash
git checkout main
git revert [commit-hash]
git push origin main
# Or revert to previous tag:
git checkout rollback-sprint-1
git checkout -b hotfix/critical-issue
# Fix issue
git merge main
```

### Rollback Documentation
```markdown
## Rollback Procedure for v1.0.0

**When to use:** If critical issues discovered post-deployment

**Rollback steps:**
1. Rollback to rollback-sprint-1 tag
2. Revert production to previous version
3. Deploy rollback-sprint-1 version
4. Notify stakeholders
5. Document incident in PROJECT_MEMORY.md

**Time to rollback:** [estimated time]
**Data preservation:** [what data is preserved]
**Verification steps:** [how to verify rollback successful]
```

## Build Artifacts & Storage

### What Gets Stored
```
/releases/
├── v1.0.0/
│   ├── website-files/
│   ├── DEPLOYMENT.md
│   ├── CHANGELOG.md
│   └── ROLLBACK.md
├── v1.0.1/
│   ├── website-files/
│   ├── DEPLOYMENT.md
│   ├── CHANGELOG.md
│   └── ROLLBACK.md
└── VERSIONS.md (index of all releases)
```

### Retention Policy
- Keep all release builds indefinitely
- Archive old preview builds after 30 days
- Keep development builds only during sprint
- Archive to `/archive/` if superseded

## Performance Metrics

### Target Metrics (to be configured)
- Page load time: < 2 seconds
- Time to interactive: < 3 seconds
- Cumulative Layout Shift: < 0.1
- Largest Contentful Paint: < 2.5 seconds
- First Input Delay: < 100ms

### Monitoring
- Deploy monitoring tools
- Track metrics over time
- Alert on regressions
- Document in build reports

## Build Documentation Template

```markdown
# Build v1.0.0 Report

## Overview
[Brief description of what's in this build]

## Features Added
- Feature 1
- Feature 2
- Feature 3

## Bugs Fixed
- Bug 1: [description]
- Bug 2: [description]

## Documentation Updates
- docs/Architecture.md: Added section on responsive design
- README.md: Updated service areas
- PROJECT_MEMORY.md: Added decision rationale

## Test Results
- Functional: ✅ Pass
- Cross-browser: ✅ Pass
- Responsive: ✅ Pass
- Performance: ✅ Pass
- Accessibility: ✅ Pass
- SEO: ✅ Pass

## Performance Metrics
- Page load: 1.8s (target: 2s) ✅
- Time to interactive: 2.1s (target: 3s) ✅
- CLS: 0.05 (target: 0.1) ✅

## Deployment Notes
[Any special deployment considerations]

## Rollback Point
- Tag: rollback-sprint-1
- Procedure: [link to rollback procedure]

## Sign-off
- Built: 2026-07-13
- Tested: [names/initials]
- Approved: [owner name]
```

---

**Related Documents:**
- PROJECT_RULES.md (operational rules)
- docs/CoordinateSystem.md (coordination framework)
- docs/Architecture.md (technical design)

**Last Updated:** 2026-07-13  
**Version:** 1.0
