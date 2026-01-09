# Debug Report: GitHub Profile README Images

**Date:** 2026-01-09
**Issue:** Images showing "?" in GitHub profile README

---

## Root Cause Analysis

### Services Status

| Service | Status | Error | Details |
|---------|--------|-------|---------|
| `github-readme-stats.vercel.app` | **DOWN** | 503 DEPLOYMENT_PAUSED | Vercel deployment paused |
| `streak-stats.demolab.com` | **PARTIAL** | 503 with long params | Works with minimal params, fails with complex styling |
| `github-readme-activity-graph.vercel.app` | **WORKING** | 200 | Fully functional |

### Broken URLs

#### 1. GitHub Stats Card (Line 64)
```
URL: https://github-readme-stats.vercel.app/api?username=Khoa280703&theme=tokyonight...
Status: 503 DEPLOYMENT_PAUSED
```

**Cause:** Main github-readme-stats service deployment paused on Vercel

#### 2. Top Languages (Line 74)
```
URL: https://github-readme-stats.vercel.app/api/top-langs/?username=Khoa280703...
Status: 503 DEPLOYMENT_PAUSED
```

**Cause:** Same as above - main service down

#### 3. Streak Stats (Line 69)
```
URL: https://streak-stats.demolab.com?user=Khoa280703&theme=tokyonight&hide_border=true&background=1A1B26&stroke=2AC3DE&ring=2AC3DE&fire=FF9E64&currStreakNum=C0CAF5&currStreakLabel=2AC3DE&sideNums=C0CAF5&sideLabels=C0CAF5&dates=565F89
Status: 503 Service Unavailable
```

**Cause:** URL parameter overload/invalid formatting. Service returns HTML error page instead of SVG.

#### 4. Typing SVG (Line 6)
```
URL: https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=22...
Status: 200 WORKING
```

**Working:** No issues

#### 5. Contribution Graph (Line 79)
```
URL: https://github-readme-activity-graph.vercel.app/graph?username=Khoa280703...
Status: 200 WORKING
```

**Working:** No issues

---

## Solutions

### Fix 1: GitHub Stats Card & Top Languages

**Replace domain:** `github-readme-stats.vercel.app` → `gh-readme-stats.vercel.app`

**Updated URLs:**
```markdown
<!-- Stats Card -->
<img src="https://gh-readme-stats.vercel.app/api?username=Khoa280703&theme=tokyonight&show_icons=true&hide_border=true&count_private=true&include_all_commits=true&bg_color=1a1b26&title_color=2AC3DE&icon_color=2AC3DE&text_color=c0caf5&border_color=1a1b26" />

<!-- Top Languages -->
<img src="https://gh-readme-stats.vercel.app/api/top-langs/?username=Khoa280703&theme=tokyonight&show_icons=true&hide_border=true&layout=compact&bg_color=1a1b26&title_color=2AC3DE&text_color=c0caf5&border_color=1a1b26&langs_count=10" />
```

**Verification:** Both URLs return 200 OK

### Fix 2: Streak Stats

**Simplify URL parameters** - remove excessive color customization:

```markdown
<img src="https://streak-stats.demolab.com?user=Khoa280703&theme=tokyonight&hide_border=true" />
```

**Or use alternative service:**
```markdown
<img src="https://github-readme-streak-stats.herokuapp.com/?user=Khoa280703&theme=tokyonight&hide_border=true" />
```

**Note:** The original URL has too many custom color parameters that may exceed service limits or use deprecated parameter names.

---

## Working Services Summary

✅ **Working:**
- Typing SVG: `readme-typing-svg.herokuapp.com`
- Contribution Graph: `github-readme-activity-graph.vercel.app`
- Alternative Stats: `gh-readme-stats.vercel.app`
- Streak Stats (minimal): `streak-stats.demolab.com`

❌ **Down:**
- GitHub Stats: `github-readme-stats.vercel.app` (DEPLOYMENT_PAUSED)

⚠️ **Partially Working:**
- Streak Stats: Works only with simplified parameters

---

## Recommended Actions

1. **Immediate:** Replace `github-readme-stats.vercel.app` with `gh-readme-stats.vercel.app` in README.md
2. **Simplify** Streak Stats URL to minimal parameters
3. **Monitor** original service status - it may be temporary outage

---

## Unresolved Questions

- Is `gh-readme-stats.vercel.app` an official mirror or temporary alternative?
- Will original `github-readme-stats.vercel.app` service be restored?
- Why does streak-stats fail with multiple color parameters?
- Are there service status pages to monitor these outages?
