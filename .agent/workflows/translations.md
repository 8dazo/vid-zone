---
description: How to add new translations and compile translation files for internationalization
---

## Overview
VidZone uses PyQt5's translation system with `.ts` (source) and `.qm` (compiled) files.
Translation files are located in `resource/translations/`.

## File Naming Convention
- `VideoCaptioner_{locale}.ts` — Qt translation source file
- `VideoCaptioner_{locale}.qm` — compiled translation file

Supported locales: `en_US`, `zh_CN`, `zh_HK`

## Steps

### 1. Extract Translatable Strings
Run the extraction script to scan all `self.tr()` calls:
```bash
cd /Users/d3v1/projects/VideoCaptioner && bash scripts/trans-extract.sh
```

### 2. Edit Translations
Edit the `.ts` files in `resource/translations/` using Qt Linguist or a text editor.
Each `<message>` block has a `<source>` (original) and `<translation>` (target) element.

### 3. Compile Translations
Compile `.ts` files to `.qm`:
```bash
cd /Users/d3v1/projects/VideoCaptioner && bash scripts/trans-compile.sh
```

### 4. How self.tr() Works
- All user-facing strings must be wrapped in `self.tr("string")`
- The `main.py` loads translations based on `cfg.language` setting
- English translations are in `VideoCaptioner_en_US.ts`

### Important Notes
- When adding new UI strings, always use `self.tr()` wrapper
- After adding new strings, re-run extract → translate → compile
- The default locale now respects the `Language.ENGLISH` setting
