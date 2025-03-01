# Main Application (app.py)

## Overview
The main application file serves as the entry point and orchestrator for the TARS-AI system. It manages the initialization and coordination of all system components.

## Key Responsibilities
1. **System Initialization**
   - Load configuration
   - Initialize module managers
   - Set up thread pools

2. **Thread Management**
   - STT processing thread
   - Discord bot thread
   - Bluetooth controller thread
   - Flask web interface thread

3. **Lifecycle Management**
   - Graceful startup
   - Error handling
   - Controlled shutdown

## Code Structure
```python
# === Standard Libraries ===
import os
import sys
import threading
from datetime import datetime

# === Custom Modules ===
from modules.module_config import load_config
from modules.module_character import CharacterManager
from modules.module_memory import MemoryManager
from modules.module_stt import STTManager
from modules.module_tts import update_tts_settings
from modules.module_btcontroller import *
from modules.module_main import initialize_managers, wake_word_callback, utterance_callback, post_utterance_callback, start_bt_controller_thread, start_discord_bot, process_discord_message_callback
from modules.module_vision import initialize_blip
from modules.module_llm import initialize_manager_llm
import modules.module_chatui
```

## Initialization Process
1. Load configuration
2. Initialize character manager
3. Set up memory system
4. Configure STT/TTS
5. Start background threads

## Thread Management
| Thread Type | Purpose | Module |
|-------------|---------|--------|
| STT | Speech-to-text processing | module_stt |
| Discord | Bot integration | module_discord |
| Bluetooth | Controller input | module_btcontroller |
| Flask | Web interface | module_chatui |

## Error Handling
- Configuration validation
- Thread exception handling
- Resource cleanup

## Integration Points
- Configuration system
- All module managers
- Hardware interfaces
- Web interface