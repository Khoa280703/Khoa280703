---
title: "GitHub Profile Enhancement - Tokyo Night Theme"
description: "Thêm banner gradient 3D, wave separators, trophy cabinet và YouTube card vào GitHub Profile với Tokyo Night theme"
status: pending
priority: P1
effort: 8h
branch: main
tags: [github-profile, tokyo-night, ui-enhancement, youtube-integration]
created: 2026-01-09
---

## Overview

Kế hoạch nâng cấp GitHub Profile với Tokyo Night theme, thêm các tính năng:
- Header banner với gradient và avatar 3D spinning
- Wave separators animated giữa sections
- Trophy cabinet hiển thị achievements
- YouTube card tự động sync videos

## Context

**Repo**: https://github.com/Khoa280703/Khoa280703
**Theme**: Tokyo Night (#2AC3DE cyan, #1A1B26 bg, #C0CAF5 text)
**Current**: Typing animation, stats, streak, snake (đã có)
**Avatar**: https://github.com/Khoa280703.png

## Phases

| Phase | Duration | Description |
|-------|----------|-------------|
| 1 | 1.5h | Header Banner - Gradient + 3D Avatar Spinning |
| 2 | 1.5h | Wave Separators - SVG Animated |
| 3 | 2h | Trophy Cabinet - GitHub Profile Trophy Integration |
| 4 | 3h | YouTube Card - GitHub Action Workflow |

## Success Criteria

- [ ] Header banner hiển thị gradient Tokyo Night với avatar 3D spinning smooth
- [ ] Wave separators animated flow giữa các sections
- [ ] Trophy cabinet hiển thị đầy đủ achievements với tokyonight theme
- [ ] YouTube card auto-sync videos từ public channel (không cần API key)
- [ ] Tất cả components responsive và performance tốt
- [ ] Code clean, well-documented, reusable

## Technical Requirements

**CSS**:
- Tokyo Night color palette
- Smooth animations (60fps target)
- Responsive design

**GitHub Actions**:
- YouTube workflow (cron + manual trigger)
- Snake workflow (existing - maintain)

**External Services**:
- github-profile-trophy.vercel.app
- YouTube public RSS feed (không API key)

## Files Structure

```
.github/
├── workflows/
│   ├── snake.yml (existing)
│   └── youtube-sync.yml (new)
README.md (update)
```

## Timeline Estimate

- Phase 1: 1.5h (banner + avatar)
- Phase 2: 1.5h (waves)
- Phase 3: 2h (trophy)
- Phase 4: 3h (youtube workflow)
- **Total: ~8h**

## Dependencies

- None (pure CSS + GitHub Actions)
- External services (CDN-based)

## References

- [Tokyo Night Theme Colors](https://github.com/folke/tokyonight.nvim)
- [GitHub Profile Trophy](https://github.com/ryo-ma/github-profile-trophy)
- [YouTube RSS Feed](https://developers.google.com/youtube/v3/docs)

---

**Chi tiết từng phase xem trong files `phase-*.md`**
