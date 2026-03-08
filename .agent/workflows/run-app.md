---
description: How to run the VidZone application locally for development
---
// turbo-all

## Steps

1. Make sure you have `uv` installed:
```bash
which uv
```

2. Install all dependencies:
```bash
cd /Users/d3v1/projects/VideoCaptioner && uv sync
```

3. Run the application:
```bash
cd /Users/d3v1/projects/VideoCaptioner && uv run python main.py
```

4. The app window should open with the dark-themed VidZone interface.
