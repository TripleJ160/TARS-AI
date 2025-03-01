# TARS-AI Documentation

## Overview
TARS-AI is a recreation of the robot TARS from Interstellar, featuring advanced AI capabilities. The system combines:
- Natural language processing
- Speech recognition and synthesis
- Physical movement control
- Computer vision
- Home automation integration

## System Architecture

### Core Components
1. **Main Application (app.py)**
   - Initializes all modules
   - Manages threads for concurrent operations
   - Handles system lifecycle

2. **Module Structure**
   - **Speech Processing**
     - STT (Speech-to-Text)
     - TTS (Text-to-Speech)
   - **Memory Management**
     - Short-term and long-term memory
     - Contextual memory retrieval
   - **Character Personality**
     - Personality traits and behaviors
     - Dynamic response generation
   - **Hardware Control**
     - Servo motor control
     - Movement coordination
   - **AI Capabilities**
     - Language model integration
     - Computer vision
     - Web search

### Configuration
System behavior is controlled through:
- `config.ini`: Main configuration file
- `persona.ini`: Character-specific settings
- `.env`: Sensitive credentials and API keys

## Hardware Integration

### Servo Control
- PCA9685 PWM controller
- Multiple servos for:
  - Torso movement (height, rotation)
  - Arm and hand movements
- Smooth motion transitions with precise timing

### Input Devices
- Bluetooth controller support
- Keyboard/mouse input handling

## Installation

### Requirements
- Python 3.8+
- System dependencies:
  - Chromium browser
  - Audio processing tools (sox, portaudio)
  - Text-to-speech engine (espeak-ng)

### Setup Process
1. Run `Install.sh` to:
   - Install system dependencies
   - Create Python virtual environment
   - Install Python packages
   - Initialize configuration files

2. Configure:
   - `config.ini` with system settings
   - `.env` with API keys and credentials

## Usage

### Starting the System
1. Activate virtual environment:
   ```bash
   source .venv/bin/activate
   ```

2. Run main application:
   ```bash
   python src/app.py
   ```

### Key Features
- Voice interaction
- Physical movement control
- AI-powered conversation
- Home automation integration
- Discord bot functionality

## Development

### Module Structure
- Each major feature is implemented as a separate module
- Modules communicate through well-defined interfaces
- Configuration-driven behavior

### Testing
- Unit tests for individual modules
- Integration tests for system behavior
- Hardware simulation for movement testing

## Troubleshooting

### Common Issues
1. **Hardware Connection Problems**
   - Verify I2C device presence
   - Check servo connections

2. **API Key Errors**
   - Ensure correct keys in `.env`
   - Verify API service availability

3. **Audio Processing Issues**
   - Check audio device configuration
   - Verify required codecs are installed

## License
TARS-AI is licensed under the [CC-BY-NC License](./LICENSE).

## Attribution
Please review the [Attribution Guidelines](./ATTRIBUTION.md) when using or modifying this project.