---
description: How to run tests, linting, and type checking
---
// turbo-all

## Run All Tests
```bash
cd /Users/d3v1/projects/VideoCaptioner && uv run pytest
```

## Run Specific Test Module
```bash
cd /Users/d3v1/projects/VideoCaptioner && uv run pytest tests/test_asr/ -v
cd /Users/d3v1/projects/VideoCaptioner && uv run pytest tests/test_translate/ -v
cd /Users/d3v1/projects/VideoCaptioner && uv run pytest tests/test_split/ -v
```

## Run Type Checking
```bash
cd /Users/d3v1/projects/VideoCaptioner && uv run pyright
```

## Run Linting
```bash
cd /Users/d3v1/projects/VideoCaptioner && uv run ruff check .
```

## Auto-fix Lint Issues
```bash
cd /Users/d3v1/projects/VideoCaptioner && uv run ruff check . --fix
```
