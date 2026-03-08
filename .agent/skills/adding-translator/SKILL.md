---
name: adding-translator
description: How to add a new translation service to VidZone
---

# Adding a New Translation Service

## Overview
Translation services implement a base translator interface and support batch translation of subtitle segments.

## Steps

### 1. Create the Translator Module
```python
# app/core/translate/my_translator.py
from app.core.translate.base import BaseTranslator

class MyTranslator(BaseTranslator):
    """My custom translator"""
    
    async def translate_batch(self, texts: list[str], target_lang: str) -> list[str]:
        # Implement batch translation
        pass
```

### 2. Register in Entities
Add to `TranslatorServiceEnum` in `app/core/entities.py`:
```python
class TranslatorServiceEnum(Enum):
    MY_TRANSLATOR = "My Translator"
```

### 3. Update Factory
Register in `app/core/translate/factory.py`.

### 4. Add Configuration
- Add API keys / endpoints to `app/common/config.py`
- Add UI settings card in `app/view/setting_interface.py`

### 5. Add Target Language Support
Check `app/core/translate/types.py` for `TargetLanguage` enum — ensure your translator maps these correctly.

### 6. Add Tests
Create `tests/test_translate/test_my_translator.py`.

## Reference Files
- Base class: `app/core/translate/base.py`
- Types: `app/core/translate/types.py`
- Factory: `app/core/translate/factory.py`
- Existing: `app/core/translate/bing_translator.py`, `app/core/translate/llm_translator.py`
