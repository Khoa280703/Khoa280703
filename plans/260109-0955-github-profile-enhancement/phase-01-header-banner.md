# Phase 01: Header Banner with 3D Spinning Avatar

## Context

Thêm header banner gradient Tokyo Night với avatar 3D spinning animation vào đầu README.md.

## Overview

- Tạo gradient banner background với Tokyo Night colors
- Thêm avatar với 3D spinning effect (CSS keyframes)
- Responsive design cho mobile/desktop

## Key Insights

- **Gradient**: Linear gradient từ #1A1B26 → #2AC3DE → #C0CAF5
- **3D Spin**: Use `transform-style: preserve-3d` + `rotateY`
- **Performance**: Use `will-change` property, GPU acceleration
- **Border**: Glow effect với `box-shadow`

## Requirements

### Visual Specs
- Banner height: 200px (desktop), 150px (mobile)
- Avatar size: 120px (desktop), 80px (mobile)
- Spin speed: 10s per rotation (smooth)
- Colors: Tokyo Night palette

### Animation Specs
- Hover: Speed up to 3s
- Glow pulse: 2s infinite
- Smooth easing: cubic-bezier

## Implementation Steps

### Step 1: Create Banner HTML Structure

```html
<!-- Header Banner -->
<div align="center">
  <div class="tokyo-banner">
    <img src="https://github.com/Khoa280703.png"
         alt="Avatar"
         class="avatar-3d"
         width="120"
         height="120" />
  </div>
</div>

<br />

<style>
/* CSS Styles */
.tokyo-banner {
  background: linear-gradient(135deg, #1A1B26 0%, #2AC3DE 50%, #C0CAF5 100%);
  padding: 40px 20px;
  border-radius: 20px;
  position: relative;
  overflow: hidden;
  margin-bottom: 20px;
}

/* Add more CSS... */
</style>
```

### Step 2: Add CSS Animation Keyframes

```css
@keyframes spin3d {
  0% { transform: rotateY(0deg); }
  100% { transform: rotateY(360deg); }
}

@keyframes glow {
  0%, 100% { box-shadow: 0 0 20px #2AC3DE; }
  50% { box-shadow: 0 0 40px #2AC3DE, 0 0 60px #C0CAF5; }
}

.avatar-3d {
  border-radius: 50%;
  border: 4px solid #2AC3DE;
  animation: spin3d 10s linear infinite, glow 2s ease-in-out infinite;
  transform-style: preserve-3d;
  will-change: transform;
  transition: animation-duration 0.3s ease;
}

.avatar-3d:hover {
  animation-duration: 3s;
}
```

### Step 3: Add Particle Effects (Optional)

```css
/* Floating particles */
.tokyo-banner::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(42, 195, 222, 0.1) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: particles 20s linear infinite;
}

@keyframes particles {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}
```

### Step 4: Position in README

Đặt banner ngay sau opening `<div align="center">` và trước typing animation.

## Todo List

- [ ] Create banner HTML structure với gradient background
- [ ] Implement 3D spinning avatar CSS animation
- [ ] Add hover effects (speed up + glow)
- [ ] Add particle background effects (optional)
- [ ] Test responsiveness mobile/desktop
- [ ] Optimize performance (will-change, GPU acceleration)
- [ ] Verify cross-browser compatibility

## Success Criteria

- [ ] Banner displays với correct Tokyo Night gradient
- [ ] Avatar spins smooth 360° (10s duration)
- [ ] Hover effect speeds up rotation (3s)
- [ ] Glow effect pulses smoothly
- [ ] Responsive on mobile (avatar 80px)
- [ ] No performance issues (60fps)
- [ ] Works in Chrome, Firefox, Safari, Edge

## Code Snippets

### Complete Banner Code

```html
<!-- Tokyo Night Header Banner -->
<div align="center">
  <div class="tokyo-banner">
    <img src="https://github.com/Khoa280703.png"
         alt="Khoa's Avatar"
         class="avatar-3d"
         width="120"
         height="120" />
  </div>
</div>

<br />

<style>
.tokyo-banner {
  background: linear-gradient(135deg, #1A1B26 0%, #2AC3DE 50%, #C0CAF5 100%);
  padding: 40px 20px;
  border-radius: 20px;
  position: relative;
  overflow: hidden;
  margin-bottom: 20px;
  box-shadow: 0 10px 40px rgba(42, 195, 222, 0.3);
}

.avatar-3d {
  border-radius: 50%;
  border: 4px solid #2AC3DE;
  animation: spin3d 10s linear infinite, glow 2s ease-in-out infinite;
  transform-style: preserve-3d;
  will-change: transform;
  transition: animation-duration 0.3s ease;
  background: #1A1B26;
}

.avatar-3d:hover {
  animation-duration: 3s;
}

@keyframes spin3d {
  0% { transform: rotateY(0deg); }
  100% { transform: rotateY(360deg); }
}

@keyframes glow {
  0%, 100% {
    box-shadow: 0 0 20px #2AC3DE, 0 0 40px rgba(42, 195, 222, 0.5);
  }
  50% {
    box-shadow: 0 0 40px #2AC3DE, 0 0 80px rgba(42, 195, 222, 0.8), 0 0 60px #C0CAF5;
  }
}

@media (max-width: 768px) {
  .tokyo-banner {
    padding: 30px 15px;
  }
  .avatar-3d {
    width: 80px;
    height: 80px;
  }
}
</style>
```

## Notes

- Test thoroughly trên mobile devices
- Consider reducing animation duration nếu quá slow
- GitHub README renders HTML/CSS nhưng limit một số properties
- Use inline styles trong `<style>` tags for GitHub compatibility
