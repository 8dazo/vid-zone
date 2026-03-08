---
name: adding-asr-engine
description: How to add a new ASR (speech recognition) engine to VidZone
---

# Adding a New ASR Engine

## Overview
ASR engines are pluggable modules in `app/core/asr/`. Each engine implements a base interface and is registered in the transcription model enum and factory.

## Steps

### 1. Create the Engine Module
Create a new file in `app/core/asr/`:
```python
# app/core/asr/my_engine.py
from app.core.asr.base import BaseASR

class MyEngine(BaseASR):
    """My custom ASR engine"""
    
    def transcribe(self, audio_path: str, language: str = "auto") -> ASRData:
        # Implement transcription logic
        # Must return ASRData with segments
        pass
```

### 2. Register in Entities
Add to `TranscribeModelEnum` in `app/core/entities.py`:
```python
class TranscribeModelEnum(Enum):
    # ... existing entries
    MY_ENGINE = "MyEngine ✨"
```

### 3. Update Factory
Update `app/core/asr/__init__.py` to include the new engine in the factory/dispatcher.

### 4. Add UI Settings (if needed)
If the engine needs configuration, add settings in:
- `app/common/config.py` — config items
- `app/view/setting_interface.py` — UI controls
- `app/components/` — custom setting widgets if complex

### 5. Add Tests
Create `tests/test_asr/test_my_engine.py` with unit tests.

## Reference Files
- Base class: `app/core/asr/base.py`
- ASR data model: `app/core/asr/asr_data.py`
- Existing engines: `app/core/asr/whisper_cpp.py`, `app/core/asr/faster_whisper.py`
