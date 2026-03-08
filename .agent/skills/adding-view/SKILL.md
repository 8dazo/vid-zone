---
name: adding-view
description: How to add a new UI view/page to VidZone
---

# Adding a New UI View

## Overview
Views are PyQt5 widgets using FluentWidgets components. Each view gets a navigation entry in the main window sidebar.

## Steps

### 1. Create the View
Create a new file in `app/view/`:
```python
# app/view/my_interface.py
from PyQt5.QtWidgets import QWidget, QVBoxLayout
from qfluentwidgets import ScrollArea

class MyInterface(ScrollArea):
    def __init__(self, parent=None):
        super().__init__(parent=parent)
        self.setObjectName("myInterface")
        self.setWindowTitle(self.tr("My Feature"))
        self._initUI()
    
    def _initUI(self):
        # Build the UI layout
        pass
```

### 2. Register in MainWindow
Update `app/view/main_window.py`:
```python
from app.view.my_interface import MyInterface

# In __init__:
self.myInterface = MyInterface(self)

# In initNavigation():
self.addSubInterface(self.myInterface, FIF.EMOJI_TAB_SYMBOLS, self.tr("My Feature"))
```

### 3. Use Signals for Communication
Use `app/common/signal_bus.py` to communicate between views:
```python
from app.common.signal_bus import signalBus
# Emit: signalBus.some_signal.emit(data)
# Connect: signalBus.some_signal.connect(self.handler)
```

### 4. Add Translations
Wrap all user-visible strings in `self.tr()`.

## UI Components Available
Check `app/components/` for reusable components:
- `MySettingCard` — custom settings cards
- `MyVideoWidget` — video player widget
- `SpinBoxSettingCard`, `LineEditSettingCard` — input cards
- `EditComboBoxSettingCard` — dropdown with edit

## Design Guidelines
- Use dark theme compatible colors
- Follow FluentWidgets component patterns
- Use `ScrollArea` as base for scrollable content pages
