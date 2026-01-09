# Phase 03: Trophy Cabinet Integration

## Context

Tích hợp GitHub Profile Trophy để hiển thị achievements và contributions với Tokyo Night theme.

## Overview

- Sử dụng `github-profile-trophy.vercel.app` service
- Display trophies với Tokyo Night theme
- Position sau GitHub Stats section
- Configurable layout và options

## Key Insights

- **Service**: Free, no API key needed, GitHub OAuth
- **Theme**: `tokyonight` được hỗ trợ native
- **Customization**: Rows, columns, margin, no-frame options
- **Performance**: CDN-hosted, auto-refresh
- **Positioning**: Best after GitHub Stats, before Snake

## Requirements

### Display Specs
- Theme: `tokyonight`
- Layout: 2 rows, 4 columns (8 trophies total)
- Show: All achievements (stars, commits, PRs, issues, etc.)
- Frame: No frame (cleaner look)
- Margin: compact spacing

### Content Specs
Trophies to display:
- Secret achievements (hidden gems)
- Multiple star levels (1k, 2k, 3k stars)
- Commit milestones
- PR/Issue achievements
- Follower milestones

## Implementation Steps

### Step 1: Generate Trophy URL

**Base URL**:
```
https://github-profile-trophy.vercel.app/?username=Khoa280703
```

**Parameters**:
- `theme=tokyonight` - Tokyo Night color scheme
- `no-frame=true` - Remove border frame
- `no-bg=false` - Keep background
- `margin-w=10` - Horizontal margin
- `margin-h=10` - Vertical margin
- `row=2` - 2 rows
- `column=4` - 4 columns

**Complete URL**:
```
https://github-profile-trophy.vercel.app/?username=Khoa280703&theme=tokyonight&no-frame=true&margin-w=10&margin-h=10&row=2&column=4
```

### Step 2: Create Trophy Section HTML

```html
<!-- Trophy Cabinet -->
<div align="center">

## 🏆 Trophy Cabinet

<p>
  <img src="https://github-profile-trophy.vercel.app/?username=Khoa280703&theme=tokyonight&no-frame=true&margin-w=10&margin-h=10&row=2&column=4"
       alt="GitHub Trophies"
       width="800" />
</p>

</div>
```

### Step 3: Position in README

Đặt Trophy Cabinet:
- **After**: GitHub Stats section
- **Before**: Snake Game section
- **Between**: Wave separators for visual flow

```markdown
## 📊 GitHub Stats
<!-- Stats cards here -->

<!-- Wave separator -->
<div class="wave-separator">...</div>

## 🏆 Trophy Cabinet
<!-- Trophy images here -->

<!-- Wave separator -->
<div class="wave-separator">...</div>

## 🐍 Snake Game
```

### Step 4: Add Custom Styling (Optional)

```html
<style>
.trophy-cabinet {
  background: linear-gradient(135deg, rgba(26, 27, 38, 0.8) 0%, rgba(42, 195, 222, 0.1) 100%);
  padding: 30px;
  border-radius: 15px;
  margin: 20px 0;
}

.trophy-cabinet img {
  max-width: 100%;
  height: auto;
  filter: drop-shadow(0 10px 20px rgba(42, 195, 222, 0.3));
}
</style>
```

### Step 5: Alternative Layout Options

**Option 1: Full Width (Single Row)**
```
&row=1&column=8
```

**Option 2: Compact (3x3)**
```
&row=3&column=3
```

**Option 3: Minimal (Top Achievements Only)**
```
&row=1&column=4&no-bg=true
```

## Todo List

- [ ] Generate correct trophy URL với Tokyo Night theme
- [ ] Create Trophy Cabinet section HTML
- [ ] Position in README (after Stats, before Snake)
- [ ] Add wave separators around trophy section
- [ ] Test display với different screen sizes
- [ ] Verify trophy data accuracy
- [ ] Add optional styling (gradient background, shadow)
- [ ] Document trophy configuration parameters

## Success Criteria

- [ ] Trophies display với Tokyo Night colors
- [ ] All 8 trophies visible in 2x4 grid
- [ ] Images load correctly from CDN
- [ ] Responsive on mobile (scales down)
- [ ] Position flows well giữa Stats và Snake
- [ ] No layout shift or overflow
- [ ] Wave separators frame the section nicely
- [ ] Page load performance acceptable

## Complete Code Snippet

```html
<!-- Trophy Cabinet Section -->
<div align="center">

## 🏆 Trophy Cabinet

<div class="trophy-cabinet">
  <img src="https://github-profile-trophy.vercel.app/?username=Khoa280703&theme=tokyonight&no-frame=true&margin-w=10&margin-h=10&row=2&column=4"
       alt="GitHub Trophies"
       width="800"
       loading="lazy" />
</div>

*Achievements unlocked through consistency and contribution*

</div>

<style>
.trophy-cabinet {
  background: linear-gradient(135deg, rgba(26, 27, 38, 0.9) 0%, rgba(42, 195, 222, 0.15) 100%);
  padding: 30px;
  border-radius: 15px;
  margin: 20px 0;
  border: 2px solid rgba(42, 195, 222, 0.3);
}

.trophy-cabinet img {
  max-width: 100%;
  height: auto;
  filter: drop-shadow(0 10px 30px rgba(42, 195, 222, 0.4));
  border-radius: 10px;
}

@media (max-width: 768px) {
  .trophy-cabinet {
    padding: 20px 10px;
  }

  .trophy-cabinet img {
    width: 100% !important;
  }
}
</style>
```

## Trophy Configuration Reference

| Parameter | Values | Default | Description |
|-----------|--------|---------|-------------|
| `theme` | tokyonight, onedark, algolia, etc. | default | Color scheme |
| `no-frame` | true, false | false | Remove border frame |
| `no-bg` | true, false | false | Remove background |
| `margin-w` | 0-30 | 15 | Horizontal spacing |
| `margin-h` | 0-30 | 15 | Vertical spacing |
| `row` | 1-4 | 1 | Number of rows |
| `column` | 1-8 | 4 | Columns per row |

## Notes

- Trophy service auto-updates từ GitHub data
- Cache expires ~24 hours
- Some achievements hidden until unlocked
- Custom themes available via CSS
- Consider adding tooltip text explaining trophy significance
- Monitor page load impact (large images)

## Troubleshooting

**Trophies not loading**:
- Check username spelling
- Verify GitHub profile is public
- Clear browser cache
- Check CDN status

**Wrong colors**:
- Verify `theme=tokyonight` parameter
- Clear GitHub README cache (hard refresh)

**Layout issues**:
- Adjust `row` and `column` parameters
- Check image width constraints
- Test on different screen sizes
