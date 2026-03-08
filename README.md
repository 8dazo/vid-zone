<div align="center">
  <h1>vid-zone</h1>
  <p>A video caption processing assistant based on Large Language Models (LLM), supporting the full workflow of speech recognition, subtitle segmentation, optimization, and translation.</p>
  
  📚 **[Online Documentation](https://weifeng2333.github.io/VideoCaptioner/)** | 🚀 **[Quick Start](https://weifeng2333.github.io/VideoCaptioner/guide/getting-started)** | ⚙️ **[Configuration Guide](https://weifeng2333.github.io/VideoCaptioner/config/llm)**
</div>

## Project Introduction

vid-zone is a simple-to-operate, low-requirement application that supports both API and local offline speech recognition. It utilizes LLMs for intelligent subtitle segmentation, correction, and translation, providing a one-click full-workflow video subtitle processing solution to give your videos stunning subtitles.

- **High Accuracy**: Supports word-level timestamps and VAD (Voice Activity Detection).
- **LLM-Powered Segmentation**: Automatically reorganizes verbatim subtitles into natural and fluent sentence paragraphs based on semantic understanding.
- **Context-Aware AI Translation**: Supports reflection and optimization mechanisms for professional and authentic translations.
- **Batch Processing**: Supports batch video subtitle synthesis to improve processing efficiency.
- **Intuitive UI**: Edits and views subtitles with real-time preview and quick editing support.

## Testing

Processing a 14-minute 1080P English TED video entirely locally with Whisper model for speech recognition, and using `gpt-5-mini` for optimization and translation to Chinese, takes about **4 minutes** in total.

The model optimization and translation cost is extremely low (less than $0.01 USD based on OpenAI's official pricing).

## Quick Start

### macOS Users

#### One-Click Install and Run (Recommended)

```bash
# Method 1: Run directly (automatically installs uv, clones the project, and installs dependencies)
curl -fsSL https://raw.githubusercontent.com/8dazo/vid-zone/main/scripts/run.sh | bash

# Method 2: Clone then run
git clone https://github.com/8dazo/vid-zone.git
cd vid-zone
./scripts/run.sh
```

The script will automatically:
1. Install the [uv](https://docs.astral.sh/uv/) package manager (if not installed).
2. Clone the project to `~/vid-zone` (if not running in the project directory).
3. Install all Python dependencies.
4. Launch the application.

<details>
<summary>Manual Installation Steps</summary>

#### 1. Install uv Package Manager

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

#### 2. Install System Dependencies (macOS)

```bash
brew install ffmpeg
```

#### 3. Clone and Run

```bash
git clone https://github.com/8dazo/vid-zone.git
cd vid-zone
uv sync          # Install dependencies
uv run python main.py  # Run the app
```

</details>

### Windows Users

#### Method 1: Using the Packaged Application (Recommended)

The software is lightweight (under 60MB) and has integrated all necessary environments. Download and run it directly.

1. Download the executable from the [Release](https://github.com/8dazo/vid-zone/releases) page.
2. Open the installation package.
3. Configure LLM API (for subtitle segmentation and correction).
4. Configure translation settings (default Microsoft translation, or use your own API Key with LLMs for better quality).
5. Configure speech recognition (default online B-interface; for non-Chinese/English languages, use local transcription).

### Developer Guide

```bash
# Install dependencies (including dev tools)
uv sync

# Run the app
uv run python main.py

# Type checking
uv run pyright

# Code linting
uv run ruff check .
```

## Basic Configuration

### 1. LLM API Configuration

LLMs are used for subtitle segmentation, optimization, and translation (if selected).
For detailed configuration, refer to the interface settings in the app. Ensure you adjust thread count according to your API provider's concurrency limits.

### 2. Translation Configuration

- **LLM Translation**: 🌟 Best quality. Uses AI models for natural, context-aware translations.
- **Microsoft Translation**: Very fast default option.
- **Google Translation**: Fast, but requires appropriate network access.

### 3. Speech Recognition Engine

- **B/J Interface**: Online, fast, supports English and Chinese.
- **WhisperCpp**: Local, supports 99 languages. Good for foreign languages.
- **fasterWhisper 👍**: Local, highly recommended for Windows. Faster with CUDA support, highly accurate timestamps.

### 4. Local Whisper Models

- Tiny/Small: Good for testing or basic English.
- Medium: Recommended for Chinese.
- Large-v2 👍: Highly recommended for general stability and quality.
- Large-v3: High quality but may sometimes repeat subtitles.

### 5. Transcript Matching

You can provide reference text (glossaries, original transcripts, or specific formatting rules) in the "Subtitle Optimization and Translation" page to assist the LLM in better correcting and translating the subtitles.

## Software Workflow

```
Speech Recognition -> Subtitle Segmentation (Optional) -> Optimization & Translation (Optional) -> Video Synthesis
```

## Project Structure

```
vid-zone/
├── app/                        # Application source code
├── resource/                   # Resources (icons, fonts, templates)
├── work-dir/                   # Work directory for processed outputs
├── AppData/                    # App data (cache, models, logs, settings)
├── scripts/                    # Installation and run scripts
├── main.py                     # Entry point
└── pyproject.toml              # Project configuration
```

## 📝 Notes

1. Subtitle segmentation uses LLMs to reorganize words into natural sentences without passing timestamp data, significantly reducing processing costs.
2. Translation utilizes the "Translate-Reflect-Translate" methodology for accurate results.
3. Providing a YouTube URL automatically downloads subtitles, saving transcription time.

## 🤝 Contributing

We welcome [Issues](https://github.com/8dazo/vid-zone/issues) and Pull Requests to help improve the project!

## 📝 Changelog

See [CHANGELOG.md](./CHANGELOG.md) for full version history.

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=8dazo/vid-zone&type=Date)](https://star-history.com/#8dazo/vid-zone&Date)
