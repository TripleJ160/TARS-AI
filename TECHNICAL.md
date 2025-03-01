# TARS-AI Technical Documentation

This document provides technical details about the TARS-AI system architecture, components, and implementation.

## Core Application Files

### app.py
Main entry point that initializes all modules and manages the system lifecycle.

```python
# Key imports
from modules.module_config import load_config
from modules.module_character import CharacterManager
from modules.module_memory import MemoryManager
from modules.module_stt import STTManager
from modules.module_tts import update_tts_settings
from modules.module_btcontroller import *
from modules.module_main import initialize_managers, wake_word_callback, utterance_callback
```

**Initialization Flow:**
1. Load configuration
2. Initialize CharacterManager and MemoryManager
3. Set up STTManager with callbacks
4. Start necessary threads (Discord, Bluetooth, Flask)
5. Initialize BLIP for vision
6. Start STT thread and main loop

### app-server.py
Flask-based API server for vision and audio processing.

**Endpoints:**
- `/caption`: Image captioning using BLIP model
- `/save_audio`: Audio transcription using Whisper

**Models:**
- BLIP for image understanding
- Whisper for speech-to-text

### app-servotester.py
Utility for calibrating and testing servo motors.

**Key Functions:**
- `set_servo_pulse(channel, pulse)`: Set servo position
- `auto_calibrate_servo(channel, is_center_servo)`: Calibrate servo range
- `set_all_servos_preset()`: Set servos to predefined positions

## Module System

### module_config.py
Handles configuration loading and validation.

```python
def load_config():
    """
    Load configuration settings from 'config.ini' and 'persona.ini' and return them as a dictionary.
    """
    # Parse the main config.ini file
    config = configparser.ConfigParser()
    config_path = os.path.join(base_dir, 'config.ini')
    config.read(config_path)
    
    # Parse the persona.ini file
    character_path = config.get("CHAR", "character_card_path")
    character_name = os.path.splitext(os.path.basename(character_path))[0]
    
    persona_config = configparser.ConfigParser()
    persona_path = os.path.join(base_dir, 'character', character_name, 'persona.ini')
    persona_config.read(persona_path)
    
    # Extract and return combined configurations
    return {
        # Configuration sections...
    }
```

### module_character.py
Manages character personality and response generation.

**Key Functions:**
- `load_character_attributes()`: Load character definition
- `load_persona_traits()`: Load personality traits
- Response generation based on character traits

### module_memory.py
Handles short-term and long-term memory management.

**Memory Types:**
- Short-term: Conversation context and recent interactions
- Long-term: Persistent knowledge and historical interactions

**Key Functions:**
- `write_longterm_memory(user_input, bot_response)`: Store interactions
- `get_related_memories(query)`: Retrieve contextual memories
- `get_shortterm_memories_recent(max_entries)`: Get recent conversation

### module_stt.py
Handles speech recognition and wake word detection.

**STT Options:**
- Whisper: High-accuracy model
- Vosk: Offline capability
- Silero: Lightweight option

**Key Functions:**
- `_detect_wake_word()`: Listen for activation phrase
- `_transcribe_utterance()`: Convert speech to text
- `voice_activity_detection_main()`: Detect speech vs. silence

### module_tts.py
Manages text-to-speech synthesis.

**TTS Options:**
- Piper: Local TTS with voice cloning
- ElevenLabs: High-quality cloud TTS
- Azure: Enterprise-grade cloud TTS
- Silero: Lightweight local TTS
- espeak: Basic local TTS

**Key Functions:**
- `generate_tts_audio(text, ttsoption)`: Generate speech audio
- `play_audio_chunks(text, config)`: Stream audio output

## Hardware Control

### module_servoctl.py
Controls servo motors for physical movement.

**Movement Types:**
- Torso height adjustment (up, neutral, down)
- Torso rotation (forward, neutral, backward)
- Arm and hand movements

**Key Functions:**
```python
def height_neutral_to_up():
    # Move torso from neutral to up position
    
def torso_neutral_to_forwards():
    # Rotate torso from neutral to forward position
    
def torso_bump():
    # Perform a quick up-down movement
```

### module_btcontroller.py
Handles Bluetooth controller input for manual control.

**Controller Actions:**
- Button mappings for movement control
- Joystick input for fine control
- Special command sequences

## Configuration System

### config.ini.template
Template for the main configuration file.

**Key Sections:**
- `[CONTROLS]`: Hardware and movement settings
- `[STT]`: Speech-to-text configuration
- `[CHAR]`: Character-specific settings
- `[LLM]`: Language model configuration
- `[TTS]`: Text-to-speech settings
- `[VISION]`: Computer vision settings
- `[SERVO]`: Servo control parameters

## Installation Scripts

### Install.sh
Main installation script with dependency management.

**Key Features:**
- System dependency installation
- Python virtual environment setup
- Configuration file initialization
- Dependency installation with retry mechanism

### App-Start.sh
Application startup script.

```bash
#!/bin/bash

# Start a full-screen terminal and execute TARS-AI
xterm -fa 'Monospace' -fs 12 -fullscreen -hold -e "
    cd .. &&
    source .venv/bin/activate &&
    python src/app.py
"
```

### App-Stop.sh
Graceful shutdown script.

```bash
killall lxterminal xterm gnome-terminal konsole mate-terminal xfce4-terminal
```

## Web Interface

### module_chatui.py
Flask-based web interface for interaction and control.

**Key Features:**
- Real-time communication via WebSockets
- Configuration management interface
- System monitoring and control

**Endpoints:**
- `/`: Main interface
- `/stream`: Audio streaming
- `/receive_user_message`: Message handling