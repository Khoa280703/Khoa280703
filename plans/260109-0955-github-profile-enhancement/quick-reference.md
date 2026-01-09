# Quick Reference Guide

## Tokyo Night Color Palette

```css
/* Background Colors */
--bg-dark: #1A1B26        /* Main background */
--bg-darker: #16161E      /* Darker sections */

/* Accent Colors */
--cyan: #2AC3DE           /* Primary accent */
--magenta: #BB9AF7        /* Secondary accent */
--blue: #7AA2F7           /* Tertiary accent */
--purple: #C0CAF5         /* Text & highlights */

/* Additional */
--orange: #FF9E64         /* Warnings/highlights */
--green: #9ece6a          /* Success */
--red: #f7768e            /* Error */
```

## URL References

### Trophy Cabinet
```
Base: https://github-profile-trophy.vercel.app/
Params: ?username=Khoa280703&theme=tokyonight&no-frame=true&row=2&column=4
```

### YouTube RSS Feed
```
Format: https://www.youtube.com/feeds/videos.xml?channel_id={CHANNEL_ID}
Example: https://www.youtube.com/feeds/videos.xml?channel_id=UCxxxxxxxxxx
```

### Avatar
```
GitHub: https://github.com/Khoa280703.png
Backup: https://avatars.githubusercontent.com/u/Khoa280703?v=4
```

## CSS Animation Keyframes

### 3D Spin (Avatar)
```css
@keyframes spin3d {
  0% { transform: rotateY(0deg); }
  100% { transform: rotateY(360deg); }
}
/* Usage: animation: spin3d 10s linear infinite; */
```

### Glow Pulse
```css
@keyframes glow {
  0%, 100% { box-shadow: 0 0 20px #2AC3DE; }
  50% { box-shadow: 0 0 40px #2AC3DE, 0 0 60px #C0CAF5; }
}
/* Usage: animation: glow 2s ease-in-out infinite; */
```

### Wave Flow
```css
@keyframes wave-flow {
  0% { transform: translateX(0); }
  50% { transform: translateX(-25%); }
  100% { transform: translateX(0); }
}
/* Usage: animation: wave-flow 8s linear infinite; */
```

## GitHub Actions Quick Commands

### Manual Trigger Workflow
```bash
# Via GitHub UI
Actions → YouTube Sync → Run workflow

# Via GitHub CLI
gh workflow run youtube-sync.yml
```

### Check Workflow Status
```bash
# List runs
gh run list --workflow=youtube-sync.yml

# View last run
gh run view --workflow=youtube-sync.yml

# Watch logs in real-time
gh run watch
```

### Debug Workflow
```bash
# Add debug output in workflow
- name: Debug
  run: |
    echo "Channel ID: ${{ secrets.YOUTUBE_CHANNEL_ID }}"
    ls -la
    cat youtube-feed.xml | head -20
```

## Image Sizes

| Component | Desktop | Mobile |
|-----------|---------|--------|
| Avatar | 120x120 | 80x80 |
| Trophy Card | Auto (800px width) | 100% width |
| YouTube Thumbnail | 320x180 | 100% width |
| Wave Height | 80px | 60px |

## Common Issues & Fixes

### Avatar Not Spinning
```css
/* Add GPU acceleration */
.avatar-3d {
  will-change: transform;
  transform: translateZ(0); /* Force GPU */
}
```

### Waves Not Animating
```css
/* Check SVG preserveAspectRatio */
svg {
  preserveAspectRatio: none; /* Allow stretch */
}
```

### Trophies Not Loading
```html
<!-- Add fallback -->
<img src="..." onerror="this.src='fallback.png'" />
```

### YouTube Thumbnails Broken
```python
# Use fallback quality
thumbnail = f"https://img.youtube.com/vi/{video_id}/hqdefault.jpg"
# Try maxresdefault → hqdefault → mqdefault
```

## Git Commands for Implementation

```bash
# Create backup branch
git checkout -b backup/readme-before-enhancement
git push origin backup/readme-before-enhancement

# Create feature branch
git checkout -b feat/github-profile-enhancement

# Commit changes
git add README.md .github/workflows/youtube-sync.yml
git commit -m "feat: add header banner, waves, trophies, youtube"

# Push and test
git push origin feat/github-profile-enhancement

# Merge to main when ready
git checkout main
git merge feat/github-profile-enhancement
git push origin main
```

## Testing Checklist

### Visual Testing
- [ ] Header banner gradient visible
- [ ] Avatar spins smoothly
- [ ] Waves animate between sections
- [ ] Trophies display correctly
- [ ] YouTube cards show thumbnails
- [ ] All colors match Tokyo Night

### Responsive Testing
- [ ] Desktop (1920x1080)
- [ ] Laptop (1366x768)
- [ ] Tablet (768x1024)
- [ ] Mobile (375x667)
- [ ] Mobile landscape (667x375)

### Browser Testing
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)

### Performance Testing
- [ ] Lighthouse score >90
- [ ] Animation 60fps
- [ ] No layout shift
- [ ] Images lazy load
- [ ] Total page load <3s

## Speed Optimization Tips

```css
/* GPU acceleration */
.animated-element {
  will-change: transform;
  transform: translateZ(0);
}

/* Smooth animations */
.animated-element {
  animation: name 10s linear infinite;
}

/* Hover effects */
.animated-element {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
```

## Markdown Escaping

```markdown
<!-- Use HTML for complex styling -->
<div class="custom">Content</div>

<!-- Escape special characters -->
\# Not a header
\* Not italic
\_ Not underscore

<!-- Use HTML entities -->
&copy; → ©
&hearts; → ♥
```

## README Best Practices

- Keep total length <500 lines
- Use semantic sections (##)
- Add comments for separators
- Use consistent spacing
- Test render before pushing
- Keep images optimized
- Use CDN for external resources

## External Resources

### Services Used
- GitHub Profile Trophy: https://github.com/ryo-ma/github-profile-trophy
- Snake Animation: https://github.com/Platane/snk
- Typing SVG: https://git.io/typing-svg
- Stats Cards: https://github.com/anuraghazra/github-readme-stats

### Documentation
- GitHub Flavored Markdown: https://guides.github.com/features/mastering-markdown/
- CSS Animations: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations
- GitHub Actions: https://docs.github.com/en/actions

---

**Need help? Check individual phase files for detailed implementation steps.**
