# VidZone (formerly VideoCaptioner)

> AI-powered video captioning desktop application built with Python, PyQt5, and FluentWidgets.

## Project Identity

| Field | Value |
|-------|-------|
| **Name** | VidZone |
| **Previous Name** | VideoCaptioner |
| **Version** | v1.4.0 |
| **License** | GPL-3.0 |
| **Python** | >=3.10, <3.13 |
| **Package Manager** | uv |
| **UI Framework** | PyQt5 + PyQt-Fluent-Widgets |
| **GitHub** | https://github.com/8dazo/vid-zone |
| **Default Language** | English |

---

## Project Rules

### Code Style
- **Linting**: Use `ruff` with rules `E, F, I, W` (ignore `E501`)
- **Type Checking**: Use `pyright` in basic mode
- **Line Length**: 100 characters max
- **Python Version Target**: 3.10+
- **Imports**: Organized by `isort` via ruff

### Architecture Rules
1. All UI views live in `app/view/` and extend FluentWidgets components
2. All background processing uses `QThread`-based workers in `app/thread/`
3. Core business logic lives in `app/core/` — never import UI in core modules
4. Configuration uses `qfluentwidgets.QConfig` via `app/common/config.py`
5. Signals for cross-component communication go through `app/common/signal_bus.py`
6. Constants and path definitions are centralized in `app/config.py`
7. All prompts for LLM interactions are in `app/core/prompts/`

### UI/UX Rules
- Default theme: **Dark mode** with accent color `#ff28f08b`
- All user-facing strings must use `self.tr()` for internationalization
- Translation files are in `resource/translations/`
- Support Chinese (Simplified/Traditional) and English locales
- Default UI language: **English**

### Testing Rules
- Tests live in `tests/` with subdirectories mirroring `app/core/`
- Use `pytest` with markers: `integration`, `slow`, `llm`, `translator`
- Run tests: `uv run pytest`
- Run type checking: `uv run pyright`
- Run linting: `uv run ruff check .`

### Dependency Rules
- Use `uv` for dependency management (not pip)
- Dependencies declared in `pyproject.toml`
- Platform-specific overrides for PyQt5-Qt5 versions
- Dev dependencies: pyright, ruff, pytest

---

## Architecture Overview

```
VidZone/
├── main.py                         # Entry point (PyQt5 app setup, i18n, DPI scaling)
├── pyproject.toml                  # Project config, dependencies, tool settings
├── app/                            # Application source code
│   ├── config.py                   # Paths, version, URLs (APP_NAME, VERSION, etc.)
│   ├── common/
│   │   ├── config.py               # QConfig settings (LLM, translate, transcribe, UI)
│   │   └── signal_bus.py           # PyQt signals for cross-component communication
│   ├── components/                 # Reusable UI components (settings cards, dialogs)
│   ├── core/                       # Business logic
│   │   ├── asr/                    # Speech recognition engines
│   │   ├── llm/                    # LLM integration (OpenAI-compatible)
│   │   ├── translate/              # Translation services
│   │   ├── tts/                    # Text-to-speech
│   │   ├── subtitle/              # Subtitle parsing/rendering
│   │   ├── split/                  # LLM-powered sentence splitting
│   │   ├── optimize/              # Subtitle optimization
│   │   ├── prompts/               # LLM prompt templates
│   │   ├── entities.py            # Enums, data classes, types
│   │   ├── task_factory.py        # Task creation and management
│   │   └── utils/                 # Logging, caching, platform utils
│   ├── thread/                    # Background processing threads
│   └── view/                      # UI pages/interfaces
├── resource/                      # Static resources
│   ├── assets/                    # Icons, logos
│   ├── fonts/                     # Bundled fonts
│   ├── subtitle_style/            # Subtitle style presets
│   └── translations/             # i18n .qm/.ts files
├── scripts/                       # Build & run scripts
├── tests/                         # Test suite
├── AppData/                       # Runtime data (logs, cache, models, settings)
└── work-dir/                      # Output directory for processed files
```

---

## Key Modules

### ASR Engines (`app/core/asr/`)
| Engine | Type | Notes |
|--------|------|-------|
| BCut (B接口) | Online API | Fast, Chinese/English only |
| Jianying (J接口) | Online API | Fast, Chinese/English only |
| WhisperCpp | Local | 99 languages, cross-platform |
| FasterWhisper | Local | Windows-optimized, CUDA support |
| Whisper API | Remote API | OpenAI-compatible endpoints |

### LLM Services (`app/core/llm/`)
OpenAI, SiliconCloud, DeepSeek, Ollama, LM Studio, Gemini, ChatGLM — all exposed via OpenAI-compatible API interface.

### Translation (`app/core/translate/`)
Bing (default), Google, DeepLX, LLM-powered (with reflect-translate methodology).

### TTS (`app/core/tts/`)
OpenAI TTS, OpenAI FM, SiliconFlow voices.

### Subtitle Processing
- **Split** (`app/core/split/`): LLM-based sentence segmentation
- **Optimize** (`app/core/optimize/`): LLM-based correction
- **Subtitle** (`app/core/subtitle/`): Parsing, rendering, ASS/SRT/VTT support
- **Synthesis**: FFmpeg-based video output with burned subtitles

---

## Development Quick Reference

```bash
# Install dependencies
uv sync

# Run the app
uv run python main.py

# Run tests
uv run pytest

# Type checking
uv run pyright

# Lint
uv run ruff check .

# Lint with auto-fix
uv run ruff check . --fix
```
