# TARS-AI Detailed Component Documentation

## Core Application Files

### app.py
- **Purpose**: Main entry point for the TARS-AI application
- **Key Responsibilities**:
  - Initialize all system modules
  - Manage application lifecycle
  - Handle thread management for concurrent operations
  - Coordinate communication between modules
- **Dependencies**:
  - All module managers (STT, TTS, Memory, Character, etc.)
  - Configuration system
- **Thread Management**:
  - STT processing thread
  - Discord bot thread
  - Bluetooth controller thread
  - Flask web interface thread

### app-server.py
- **Purpose**: Flask-based API server for vision and audio processing
- **Endpoints**:
  - `/caption`: Image captioning using BLIP model
  - `/save_audio`: Audio transcription using Whisper
- **Models**:
  - BLIP for image understanding
  - Whisper for speech-to-text
- **Configuration**:
  - Model size selection
  - Device optimization (CPU/GPU)
  - Compute type settings

### app-servotester.py
- **Purpose**: Servo calibration and testing utility
- **Features**:
  - Manual servo control
  - Auto-calibration for servo positions
  - Preset configurations
  - Safety checks and warnings
- **Key Functions**:
  - set_servo_pulse()
  - auto_calibrate_servo()
  - set_all_servos_preset()

## Module System (modules/)

### Core Modules
1. **module_config.py**
   - Configuration loading and management
   - Environment variable handling
   - Configuration validation

2. **module_character.py**
   - Character personality management
   - Response generation
   - Voice customization

3. **module_memory.py**
   - Short-term and long-term memory
   - Contextual memory retrieval
   - Memory persistence

4. **module_stt.py**
   - Speech-to-text processing
   - Wake word detection
   - Audio stream handling

5. **module_tts.py**
   - Text-to-speech synthesis
   - Multiple TTS engine support
   - Voice modulation

### Integration Modules
1. **module_btcontroller.py**
   - Bluetooth controller integration
   - Movement control
   - Input handling

2. **module_discord.py**
   - Discord bot integration
   - Message processing
   - Voice channel support

3. **module_homeassistant.py**
   - Home Assistant integration
   - Smart home control
   - Automation triggers

## Configuration System

### config.ini.template
- **Structure**:
  - [CONTROLS]: Hardware and movement settings
  - [STT]: Speech-to-text configuration
  - [CHAR]: Character-specific settings
  - [LLM]: Language model configuration
  - [TTS]: Text-to-speech settings
  - [VISION]: Computer vision settings
  - [SERVO]: Servo control parameters
- **Key Features**:
  - Modular configuration sections
  - Environment variable support
  - Default value management

## Installation and Startup

### App-Install-Helper.sh
- **Purpose**: Automated installation script
- **Features**:
  - System dependency installation
  - Python virtual environment setup
  - Configuration file initialization
  - Dependency installation with retry mechanism

### App-Start.sh
- **Purpose**: Application startup script
- **Features**:
  - Full-screen terminal launch
  - Virtual environment activation
  - Application execution

### App-Stop.sh
- **Purpose**: Graceful shutdown
- **Features**:
  - Process termination
  - Thread cleanup
  - Resource release

## Character System (character/)

### Structure
- Character definition files (JSON)
- Personality traits
- Voice profiles
- Response patterns

### Key Features
- Dynamic personality adaptation
- Context-aware responses
- Multi-character support

## Memory System (memory/)

### Components
1. **Short-term Memory**
   - Conversation context
   - Recent interactions
   - Temporary data storage

2. **Long-term Memory**
   - Persistent knowledge
   - Historical interactions
   - Fact storage

### Features
- Contextual retrieval
- Memory persistence
- Search and filtering

## Engine System (engine/)

### Components
1. **Training System**
   - Model training
   - Data preprocessing
   - Performance evaluation

2. **Inference System**
   - Model execution
   - Real-time processing
   - Resource optimization

## Web Interface (www/)

### Structure
- Flask-based web server
- REST API endpoints
- WebSocket support

### Features
- Real-time interaction
- Configuration management
- System monitoring