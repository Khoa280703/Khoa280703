# Phase 02: Animated Wave Separators

## Context

Thêm SVG wave separators animated giữa các sections của README.md với Tokyo Night colors.

## Overview

- Tạo SVG wave shapes với gradient fills
- Animate waves để tạo "flowing" effect
- Đặt giữa các major sections (About, Tech Stack, Stats, Snake)
- Responsive design cho all screen sizes

## Key Insights

- **SVG Path**: Use cubic bezier curves cho smooth waves
- **Animation**: CSS `transform: translateX()` cho flowing effect
- **Layering**: 2-3 wave layers với parallax speeds
- **Performance**: Use `transform` instead of `position` changes
- **Colors**: Gradient từ transparent → Tokyo Night colors

## Requirements

### Visual Specs
- Wave height: 60-80px
- Layers: 3 waves với opacity khác nhau
- Colors: #2AC3DE, #C0CAF5, #7AA2F7 (Tokyo Night)
- Animation: Smooth infinite flow

### Animation Specs
- Front wave: 8s duration
- Middle wave: 12s duration
- Back wave: 16s duration
- Direction: Left to right

## Implementation Steps

### Step 1: Create SVG Wave Component

```html
<!-- Wave Separator -->
<div class="wave-separator">
  <svg viewBox="0 0 1200 120" preserveAspectRatio="none">
    <path d="M0,0V46.29c47,0,47-46.29,94-46.29s47,46.29,94,46.29,47-46.29,94-46.29,47,46.29,94,46.29,47-46.29,94-46.29,47,46.29,94,46.29,47-46.29,94-46.29,47,46.29,94,46.29,47-46.29,94-46.29,47,46.29,94,46.29,47-46.29,94-46.29,47,46.29,94,46.29V0Z"
          fill="url(#gradient1)"
          class="wave wave1"></path>
    <path d="M0,0V15.81C13,15.81,13,32,26,32s13-16.19,26-16.19,13,16.19,26,16.19S52,16,65,16s13,16.19,26,16.19S104,16,117,16s13,16.19,26,16.19,13-16.19,26-16.19S156,32,169,32s13-16.19,26-16.19S208,32,221,32s13-16.19,26-16.19S260,32,273,32s13-16.19,26-16.19,13,16.19,26,16.19S338,16,351,16s13,16.19,26,16.19S390,16,403,16s13,16.19,26,16.19S442,32,455,32s13-16.19,26-16.19S520,32,533,32s13-16.19,26-16.19S572,32,585,32s13-16.19,26-16.19S624,16,637,16s13,16.19,26,16.19S676,16,689,16s13,16.19,26,16.19S728,32,741,32s13-16.19,26-16.19S780,32,793,32s13-16.19,26-16.19S832,16,845,16s13,16.19,26,16.19S884,16,897,16s13,16.19,26,16.19S936,32,949,32s13-16.19,26-16.19S988,32,1001,32s13-16.19,26-16.19S1040,32,1053,32s13-16.19,26-16.19S1092,16,1105,16s13,16.19,26,16.19S1144,16,1157,16s13,16.19,26,16.19V0Z"
          fill="url(#gradient2)"
          class="wave wave2"></path>
    <defs>
      <linearGradient id="gradient1" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" style="stop-color:#2AC3DE;stop-opacity:1" />
        <stop offset="100%" style="stop-color:#C0CAF5;stop-opacity:1" />
      </linearGradient>
      <linearGradient id="gradient2" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" style="stop-color:#7AA2F7;stop-opacity:0.6" />
        <stop offset="100%" style="stop-color:#2AC3DE;stop-opacity:0.6" />
      </linearGradient>
    </defs>
  </svg>
</div>
```

### Step 2: Add CSS Animation

```css
.wave-separator {
  width: 100%;
  overflow: hidden;
  line-height: 0;
  margin: 30px 0;
}

.wave-separator svg {
  display: block;
  width: 100%;
  height: 80px;
}

.wave {
  animation: wave-flow 8s linear infinite;
}

.wave2 {
  animation: wave-flow 12s linear infinite reverse;
}

@keyframes wave-flow {
  0% { transform: translateX(0); }
  50% { transform: translateX(-25%); }
  100% { transform: translateX(0); }
}
```

### Step 3: Create Wave Variants

Tạo 3 variants với different styles:

**Variant 1: Full Width Wave**
```html
<!-- Dùng cho major section breaks -->
```

**Variant 2: Center Wave**
```html
<!-- Dùng cho smaller breaks -->
```

**Variant 3: Double Wave**
```html
<!-- Dùng cho emphasized transitions -->
```

### Step 4: Insert into README Positions

```markdown
<!-- After "About Me" section -->
<div class="wave-separator">...</div>

## 🛠️ Tech Stack

<!-- After "Tech Stack" section -->
<div class="wave-separator">...</div>

## 📊 GitHub Stats
```

## Todo List

- [ ] Create SVG wave component với gradient fills
- [ ] Implement CSS animation (3 layers, parallax)
- [ ] Create 3 wave variants (full, center, double)
- [ ] Insert waves at strategic positions in README
- [ ] Test animation smoothness (60fps target)
- [ ] Optimize for mobile responsiveness
- [ ] Verify Tokyo Night color consistency

## Success Criteria

- [ ] Waves animate smoothly without lag
- [ ] Colors match Tokyo Night theme
- [ ] Parallax effect visible (3 layers)
- [ ] Responsive on all screen sizes
- [ ] No layout shift or overflow issues
- [ ] Animations loop seamlessly
- [ ] Performance optimized (GPU acceleration)

## Complete Code Snippet

```html
<!-- Wave Separator -->
<div class="wave-separator">
  <svg viewBox="0 0 1200 120" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <linearGradient id="waveGradient1" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" style="stop-color:#2AC3DE;stop-opacity:1" />
        <stop offset="50%" style="stop-color:#7AA2F7;stop-opacity:1" />
        <stop offset="100%" style="stop-color:#C0CAF5;stop-opacity:1" />
      </linearGradient>
      <linearGradient id="waveGradient2" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" style="stop-color:#C0CAF5;stop-opacity:0.7" />
        <stop offset="100%" style="stop-color:#2AC3DE;stop-opacity:0.7" />
      </linearGradient>
    </defs>
    <path d="M0,60 C150,120 350,0 600,60 C850,120 1050,0 1200,60 L1200,120 L0,120 Z"
          fill="url(#waveGradient1)"
          class="wave wave1"></path>
    <path d="M0,80 C200,140 400,20 600,80 C800,140 1000,20 1200,80 L1200,120 L0,120 Z"
          fill="url(#waveGradient2)"
          class="wave wave2"></path>
  </svg>
</div>

<style>
.wave-separator {
  width: 100%;
  overflow: hidden;
  line-height: 0;
  margin: 40px 0;
  position: relative;
}

.wave-separator svg {
  display: block;
  width: 100%;
  height: 100px;
}

.wave1 {
  animation: wave-move 8s ease-in-out infinite;
}

.wave2 {
  animation: wave-move 12s ease-in-out infinite reverse;
  opacity: 0.7;
}

@keyframes wave-move {
  0%, 100% {
    transform: translateX(0) translateY(0);
  }
  25% {
    transform: translateX(-2%) translateY(-3px);
  }
  50% {
    transform: translateX(0) translateY(-5px);
  }
  75% {
    transform: translateX(2%) translateY(-3px);
  }
}

@media (max-width: 768px) {
  .wave-separator svg {
    height: 60px;
  }
}
</style>
```

## Notes

- SVG paths cần smooth curves (cubic bezier)
- Test cross-browser compatibility
- GitHub renders SVG nhưng check inline CSS support
- Consider fallback solid color nếu SVG fails
- Optimize SVG file size (remove unnecessary metadata)
