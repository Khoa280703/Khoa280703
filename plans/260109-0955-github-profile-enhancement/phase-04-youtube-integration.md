# Phase 04: YouTube Card Integration

## Context

Tự động sync recent videos từ YouTube public channel vào GitHub Profile sử dụng GitHub Actions - KHÔNG cần API key.

## Overview

- Tạo GitHub Action workflow để fetch YouTube videos
- Parse từ YouTube RSS feed (public, no auth needed)
- Generate card/video list trong README
- Auto-update trên schedule (cron) + manual trigger
- Zero cost, no API keys required

## Key Insights

- **No API Key**: YouTube channel RSS feed is public
- **RSS URL**: `https://www.youtube.com/feeds/videos.xml?channel_id=CHANNEL_ID`
- **GitHub Actions**: Free cho public repos
- **Workflow**: Parse XML → Generate Markdown → Commit to README
- **Channel ID**: Get from URL hoặc YouTube settings

## Requirements

### Technical Specs
- Trigger: Cron (daily 12:00 UTC) + manual workflow_dispatch
- Parse: YouTube RSS XML feed
- Extract: Video title, thumbnail, URL, published date
- Limit: Display 3-6 most recent videos
- Format: Card layout hoặc list view

### Visual Specs
- Card size: 320x180 (thumbnail)
- Layout: 3 columns (desktop), 1 column (mobile)
- Tokyo Night theme colors
- Hover effects: Scale + glow

## Implementation Steps

### Step 1: Get YouTube Channel ID

**Method 1: From URL**
```
YouTube URL: https://www.youtube.com/@YOUR_CHANNEL
View Source → Search "channelId"
```

**Method 2: Use API (optional)**
```
https://www.youtube.com/oembed?url=CHANNEL_URL&format=json
```

**Example**:
```
Channel ID: UCxxxxxxxxxxxxxxxxxx
```

### Step 2: Create GitHub Action Workflow

File: `.github/workflows/youtube-sync.yml`

```yaml
name: Sync YouTube Videos

on:
  schedule:
    # Runs at 12:00 UTC every day
    - cron: "0 12 * * *"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  sync-youtube:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Fetch YouTube videos
        id: fetch-videos
        run: |
          CHANNEL_ID="${{ secrets.YOUTUBE_CHANNEL_ID }}"
          RSS_URL="https://www.youtube.com/feeds/videos.xml?channel_id=${CHANNEL_ID}"

          # Fetch RSS feed
          curl -s "${RSS_URL}" > youtube-feed.xml

          # Parse XML and extract video data
          python3 << 'EOF'
          import xml.etree.ElementTree as ET
          from datetime import datetime

          tree = ET.parse('youtube-feed.xml')
          root = tree.getroot()

          # Define namespace
          ns = {'atom': 'http://www.w3.org/2005/Atom',
                'yt': 'http://www.youtube.com/xml/schemas/2015',
                'media': 'http://search.yahoo.com/mrss/'}

          # Extract video entries
          videos = []
          for entry in root.findall('atom:entry', ns)[:6]:  # Get 6 recent videos
              video_id = entry.find('yt:videoId', ns).text
              title = entry.find('atom:title', ns).text
              published = entry.find('atom:published', ns).text
              link = entry.find('atom:link', ns).attrib['href']

              # Get thumbnail URL
              thumbnail = f"https://img.youtube.com/vi/{video_id}/maxresdefault.jpg"

              videos.append({
                  'title': title,
                  'thumbnail': thumbnail,
                  'url': link,
                  'published': published[:10]
              })

          # Generate markdown
          markdown = "<!-- START YOUTUBE -->\n"
          markdown += "## 🎬 Latest Videos\n\n"
          markdown += "<div align='center'>\n\n"

          for i, video in enumerate(videos, 1):
              markdown += f"### [{i}. {video['title']}]({video['url']})\n\n"
              markdown += f"<a href='{video['url}' target='_blank'>\n"
              markdown += f"  <img src='{video['thumbnail']}'\n"
              markdown += f"       alt='{video['title']}'\n"
              markdown += f"       width='320'\n"
              markdown += f"       style='border-radius:10px; margin:10px;' />\n"
              markdown += f"</a>\n\n"
              markdown += f"*Published: {video['published']}*\n\n"
              markdown += "---\n\n"

          markdown += "</div>\n"
          markdown += "<!-- END YOUTUBE -->\n"

          with open('youtube-videos.md', 'w') as f:
              f.write(markdown)

          print(f"Generated {len(videos)} video cards")
          EOF

      - name: Update README
        run: |
          # Remove old YouTube section
          sed -i '/<!-- START YOUTUBE -->/,/<!-- END YOUTUBE -->/d' README.md

          # Insert new YouTube section before Snake section
          sed -i '/## 🐍 Snake Game/e cat youtube-videos.md' README.md

      - name: Commit changes
        run: |
          git config --local user.email "github-actions[bot]@users.noreply.github.com"
          git config --local user.name "github-actions[bot]"
          git add README.md
          git diff --quiet && git diff --staged --quiet || git commit -m "feat: sync latest YouTube videos [skip ci]"
          git push
```

### Step 3: Add Repository Secret

1. Go to repo → Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `YOUTUBE_CHANNEL_ID`
4. Value: `YOUR_CHANNEL_ID` (e.g., `UCxxxxxxxxxxxxxxxxxx`)

### Step 4: Add Placeholder in README

```markdown
<!-- START YOUTUBE -->
## 🎬 Latest Videos

<div align="center">

*YouTube videos will be synced here automatically*

</div>
<!-- END YOUTUBE -->

---
```

### Step 5: Create Enhanced Card Styling

Add to README:

```html
<style>
.youtube-card {
  display: inline-block;
  margin: 10px;
  border-radius: 15px;
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border: 2px solid #2AC3DE;
}

.youtube-card:hover {
  transform: scale(1.05) translateY(-5px);
  box-shadow: 0 10px 30px rgba(42, 195, 222, 0.5);
}

.youtube-card img {
  display: block;
  width: 320px;
  height: 180px;
  object-fit: cover;
}

@media (max-width: 768px) {
  .youtube-card img {
    width: 100%;
    max-width: 320px;
  }
}
</style>
```

## Todo List

- [ ] Get YouTube Channel ID
- [ ] Create GitHub Action workflow file
- [ ] Add YOUTUBE_CHANNEL_ID secret to repo
- [ ] Add placeholder section in README
- [ ] Test workflow manually (workflow_dispatch)
- [ ] Verify RSS feed parsing
- [ ] Check video card generation
- [ ] Test responsive layout mobile
- [ ] Verify auto-commit works
- [ ] Monitor cron schedule execution
- [ ] Add Tokyo Night styling

## Success Criteria

- [ ] Workflow runs successfully (manual + cron)
- [ ] Fetches latest videos from RSS feed
- [ ] Generates proper markdown with cards
- [ ] Updates README automatically
- [ ] Commits pushed with "[skip ci]"
- [ ] Videos display với Tokyo Night theme
- [ ] Responsive layout mobile/desktop
- [ ] Hover effects work smoothly
- [ ] No API keys required
- [ ] Runs daily without errors

## Complete Workflow File

```yaml
name: Sync YouTube Videos

on:
  schedule:
    - cron: "0 12 * * *"  # Daily at 12:00 UTC
  workflow_dispatch:

permissions:
  contents: write

jobs:
  sync:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'

      - name: Fetch & Parse YouTube RSS
        env:
          CHANNEL_ID: ${{ secrets.YOUTUBE_CHANNEL_ID }}
        run: |
          python3 << 'PYEOF'
          import urllib.request
          import xml.etree.ElementTree as ET
          from datetime import datetime

          # Fetch RSS feed
          rss_url = f"https://www.youtube.com/feeds/videos.xml?channel_id={os.environ['CHANNEL_ID']}"
          with urllib.request.urlopen(rss_url) as response:
              xml_data = response.read()

          # Parse XML
          root = ET.fromstring(xml_data)
          ns = {'atom': 'http://www.w3.org/2005/Atom',
                'yt': 'http://www.youtube.com/xml/schemas/2015',
                'media': 'http://search.yahoo.com/mrss/'}

          # Extract 6 most recent videos
          videos = []
          for entry in root.findall('atom:entry', ns)[:6]:
              video_id = entry.find('yt:videoId', ns).text
              title = entry.find('atom:title', ns).text
              link = entry.find('atom:link', ns).attrib['href']
              published = entry.find('atom:published', ns).text[:10]
              thumbnail = f"https://img.youtube.com/vi/{video_id}/maxresdefault.jpg"

              videos.append({'title': title, 'thumbnail': thumbnail,
                           'url': link, 'published': published})

          # Generate markdown
          md = "<!-- START YOUTUBE -->\n\n"
          md += "## 🎬 Latest Videos\n\n"
          md += "<div align='center'>\n\n"

          for v in videos:
              md += f"<a href='{v['url']}' class='youtube-link'>\n"
              md += f"<img src='{v['thumbnail']}' alt='{v['title']}' "
              md += f"class='youtube-card' width='320' />\n"
              md += f"</a>\n\n"
              md += f"**[{v['title']}]({v['url']})**\n\n"
              md += f"*{v['published']}*\n\n---\n\n"

          md += "</div>\n\n<!-- END YOUTUBE -->\n"

          with open('youtube-section.md', 'w') as f:
              f.write(md)

          print(f"✅ Synced {len(videos)} videos")
          PYEOF

      - name: Update README
        run: |
          # Remove old section
          sed -i '/<!-- START YOUTUBE -->/,/<!-- END YOUTUBE -->/d' README.md
          # Insert before Snake section
          sed -i '/## 🐍 Snake Game/e cat youtube-section.md' README.md

      - name: Commit & Push
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add README.md
          git diff --quiet && git diff --staged --quiet || \
          (git commit -m "feat: sync YouTube videos [skip ci]" && git push)
```

## RSS Feed Structure

```xml
<feed xmlns="http://www.w3.org/2005/Atom">
  <entry>
    <yt:videoId>VIDEO_ID</yt:videoId>
    <title>Video Title</title>
    <link href="https://www.youtube.com/watch?v=VIDEO_ID"/>
    <published>2026-01-09T00:00:00+00:00</published>
    <media:group>
      <media:thumbnail url="THUMBNAIL_URL"/>
    </media:group>
  </entry>
</feed>
```

## Alternative: Use Existing Action

**Option: Use `gautamkrishnar/blog-post-workflow`** (modified):

```yaml
- name: Generate YouTube Section
  uses: gautamkrishnar/blog-post-workflow@v1
  with:
    comment_tag_name: "YOUTUBE"
    feed_list: "https://www.youtube.com/feeds/videos.xml?channel_id=${{ secrets.YOUTUBE_CHANNEL_ID }}"
    max_post_count: 6
    template: "<a href='{{link}}'><img src='https://img.youtube.com/vi/{{video_id}}/maxresdefault.jpg' width='320' /></a>"
```

## Notes

- RSS feed is public, no auth needed
- Channel ID ≠ Channel name/URL
- Thumbnail quality: maxresdefault > sddefault > hqdefault
- Workflow runs free on public repos
- Manual trigger available via Actions tab
- `[skip ci]` prevents workflow loop
- Test thumbnail fallback if maxres not available

## Troubleshooting

**Workflow fails**:
- Verify channel ID is correct
- Check RSS feed accessible in browser
- Review Actions logs for errors

**No videos appear**:
- Channel has 0 public videos
- Wrong channel ID
- XML parsing error

**Thumbnails broken**:
- Use `hqdefault.jpg` fallback
- Check if videos have thumbnails
- Verify img.youtube.com accessible

**Commit not pushed**:
- Check permissions in workflow
- Verify branch is not protected
- Check git config in workflow
