# 🎬 Video Creator Plugin for Claude Code

**Turn raw clips into platform-ready Reels, Shorts, and posts — with AI thumbnail generation.**

> Created by **Akshay Bhimani** | Version 1.0.0 | License: MIT

---

## What Is It?

**Video Creator** is a Claude Code plugin that brings a full video editing workflow directly into your Claude chat. Upload your raw footage, tell Claude what you want, and it handles the rest — merging, trimming, exporting for social media, and generating click-worthy thumbnails using frame-by-frame AI analysis.

No video editing software needed. No complicated timelines. Just chat with Claude.

---

## Features

| Feature | Description |
|---|---|
| 🔀 **Merge Clips** | Combine multiple video files into one seamless video |
| ✂️ **Trim & Cut** | Cut any segment from a video with frame-accurate precision |
| 🎯 **Platform Export** | One-click export optimized for Instagram, YouTube, TikTok, Facebook, Twitter |
| 🖼️ **AI Thumbnail** | Scans every frame, selects the best moment, generates a professional thumbnail |
| 📤 **GitHub Upload** | Upload your thumbnail to GitHub instantly for public sharing |
| 📊 **Video Analysis** | Get full metadata (resolution, duration, codec, bitrate) for any video |
| 🎨 **Text Overlay** | Add title text to thumbnails (requires Pillow) |

---

## Platform Support

| Platform | Resolution | Aspect Ratio | Max Duration |
|---|---|---|---|
| Instagram Reels | 1080×1920 | 9:16 vertical | 60 sec |
| TikTok | 1080×1920 | 9:16 vertical | 60 sec |
| YouTube Shorts | 1080×1920 | 9:16 vertical | 60 sec |
| YouTube | 1920×1080 | 16:9 landscape | Unlimited |
| Facebook Reels | 1080×1920 | 9:16 vertical | 60 sec |
| Twitter / X | 1280×720 | 16:9 | 140 sec |

---

## Requirements

### Required
- **[Claude Code](https://claude.ai/code)** — Claude's agentic coding environment (desktop app or VS Code)
- **[FFmpeg](https://ffmpeg.org/download.html)** — Free, open-source video processor

### Optional (for enhanced thumbnails)
- **Python 3.8+** — For the thumbnail analysis scripts
- **Pillow** — For text overlay on thumbnails (`pip install Pillow`)

---

## Installation

### Step 1 — Install FFmpeg

If you don't have FFmpeg yet:
1. Download from [ffmpeg.org/download.html](https://ffmpeg.org/download.html)
2. Extract to a folder (e.g. `C:\ffmpeg\`)
3. Note the path to `ffmpeg.exe`

The plugin is pre-configured for:
```
C:\Users\BAPS\Downloads\ffmpeg\ffmpeg-master-latest-win64-gpl\bin\ffmpeg.exe
```

To use a different path, set the environment variable:
```bash
set FFMPEG_PATH=C:\your\path\to\ffmpeg.exe
```

### Step 2 — Install the Plugin

#### Method A — Using the install script (Windows)
```
Double-click: install.bat
```

#### Method B — Manual install
1. Copy this folder to your Claude Code plugins directory:
   ```
   %APPDATA%\Claude\plugins\video-creator\
   ```
2. Restart Claude Code
3. The plugin appears under **Plugins → Local → Video Creator**

#### Method C — Via Claude Code UI
1. Open Claude Code
2. Go to **Plugins** (sidebar icon)
3. Click **+** → **Install from folder**
4. Select this `video-creator plugin` folder

### Step 3 — Verify Installation
In Claude Code chat, type:
```
/video-creator
```
Claude should greet you with the Video Creator menu.

---

## How to Use

### Basic Usage

1. Open Claude Code (desktop or VS Code)
2. Type `/video-creator` in the chat
3. Upload your video file(s)
4. Tell Claude what you want:
   - *"Merge these 3 clips into one Reel"*
   - *"Trim from 0:30 to 1:00"*
   - *"Export this for YouTube Shorts"*
   - *"Generate a thumbnail for YouTube"*

### Example Conversations

**Merge clips for Instagram:**
```
/video-creator
[upload: clip1.mp4, clip2.mp4, clip3.mp4]
"Merge all three clips and export as an Instagram Reel"
```

**Export existing video:**
```
/video-creator
[upload: my_video.mp4]
"Export this for YouTube Shorts and generate a thumbnail"
```

**Generate thumbnail only:**
```
/video-creator
[upload: finished_video.mp4]
"Just generate a YouTube thumbnail for this video"
```

**Full workflow:**
```
/video-creator
[upload: raw_footage.mp4]
"Trim from 0:15 to 0:45, export for TikTok, generate a thumbnail, and upload it to GitHub"
```

---

## Thumbnail Generation — How It Works

1. **Frame Extraction** — FFmpeg extracts one frame every 2 seconds from your video
2. **AI Analysis** — Claude examines each frame, scoring for:
   - Brightness and lighting quality
   - Sharpness / focus
   - Visual interest and composition
   - Peak action or emotional moments
3. **Best Frame Selection** — The highest-scoring frame is selected
4. **Platform Resize** — The frame is resized to exact platform dimensions
5. **Optional Text Overlay** — Add a title text bar (requires Pillow)
6. **Optional GitHub Upload** — Publish the thumbnail publicly in seconds

---

## GitHub Thumbnail Upload

After generating a thumbnail, Claude will ask:
> *"Would you like to upload this thumbnail to GitHub?"*

If yes, provide:
1. Your **GitHub Personal Access Token** (with `repo` scope)
   - Create one at: [github.com/settings/tokens](https://github.com/settings/tokens)
2. Your **repository name** (e.g. `myusername/my-thumbnails`)
3. A **filename** for the thumbnail

The thumbnail will be committed and you'll receive a public raw URL like:
```
https://raw.githubusercontent.com/username/repo/main/thumbnails/thumb.jpg
```

---

## Scripts Reference

Run scripts directly from the terminal:

```bash
# Merge clips
python scripts/video_processor.py merge \
  --inputs clip1.mp4 clip2.mp4 clip3.mp4 \
  --output merged.mp4

# Trim video
python scripts/video_processor.py trim \
  --input video.mp4 --output trimmed.mp4 \
  --start 00:00:30 --end 00:01:00

# Export for platform
python scripts/video_processor.py export \
  --input video.mp4 --output reel.mp4 \
  --platform instagram_reels

# Extract frames
python scripts/video_processor.py frames \
  --input video.mp4 --output-dir ./frames

# Generate thumbnail
python scripts/generate_thumbnail.py \
  --video video.mp4 \
  --output thumbnail.jpg \
  --platform youtube \
  --title "My Awesome Video"

# Upload thumbnail to GitHub
python scripts/github_upload.py \
  --token YOUR_GITHUB_TOKEN \
  --repo username/my-thumbnails \
  --file thumbnail.jpg \
  --filename thumbnails/my-thumb.jpg
```

---

## Useful For

- 📱 **Content Creators** — Batch-process raw footage into platform-ready Reels
- 🎥 **YouTubers** — Export and thumbnail in seconds, no Premiere needed
- 📣 **Social Media Managers** — Repurpose one video across all platforms
- 🎓 **Students / Beginners** — Learn FFmpeg through guided Claude conversations
- 🏢 **Small Businesses** — Create polished video content without a video editor

---

## Troubleshooting

### `/video-creator` command not showing
- Restart Claude Code after installing
- Check the plugin is in the correct plugins folder
- Verify `manifest.json` is present in the plugin root

### FFmpeg not found
- Run `install.bat` to set up the path
- Or manually set: `set FFMPEG_PATH=C:\path\to\ffmpeg.exe`

### Clips won't merge cleanly
- Try asking Claude to use re-encode mode: *"merge with re-encode"*
- Ensure all clips have the same frame rate

### Thumbnail looks blurry
- The video may be low resolution — thumbnail quality depends on source
- Try `--frame-count 30` for more candidate frames

### GitHub upload fails with 401
- Your token has expired or lacks `repo` scope
- Generate a new token at github.com/settings/tokens

---

## Plugin Structure

```
video-creator plugin/
├── manifest.json              # Plugin metadata
├── commands/
│   └── video-creator.md       # /video-creator command
├── skills/
│   └── video-creator.md       # AI skill: teaches Claude how to process video
├── scripts/
│   ├── video_processor.py     # Merge, trim, export via FFmpeg
│   ├── generate_thumbnail.py  # AI frame selection + thumbnail export
│   └── github_upload.py       # GitHub REST API uploader
├── install.bat                # Windows auto-installer
└── README.md                  # This file
```

---

## License

MIT License — free to use, modify, and share.

---

## Credits

**Created by Akshay Bhimani**

Built with:
- [FFmpeg](https://ffmpeg.org/) — Video processing engine
- [Claude Code](https://claude.ai/code) — Agentic AI assistant
- [GitHub REST API](https://docs.github.com/en/rest) — Thumbnail hosting
- [Pillow](https://python-pillow.org/) — Image processing (optional)

---

*Video Creator Plugin v1.0.0 — Making video creation effortless, one clip at a time.*
