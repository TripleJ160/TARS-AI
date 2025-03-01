# TARS-AI

<p align="center">
    <a href="https://discord.gg/AmE2Gv9EUt">
      <img alt="Discord Invitation Link" src="https://dcbadge.vercel.app/api/server/uXkqkz3mJJ?style=flat" align="center" />
    </a>
    <a href="https://www.youtube.com/@TARS-AI.py.youtube">
        <img src="https://img.shields.io/badge/YouTube-red?style=flat-square&logo=youtube&logoColor=white" alt="YouTube" align="center" />
    </a>
    <a href="https://www.instagram.com/tars_ai.py">
        <img src="https://img.shields.io/badge/Instagram-purple?style=flat-square&logo=instagram&logoColor=white" alt="Instagram" align="center" />
    </a>
    <a href="https://www.tiktok.com/@tars.ai.py">
        <img src="https://img.shields.io/badge/TikTok-black?style=flat-square&logo=tiktok&logoColor=white" alt="TikTok" align="center" />   
    </a>
    <a href="https://docs-tars-ai.vercel.app">
        <img src="https://img.shields.io/badge/Docs-grey?style=flat-square&logo=readthedocs&logoColor=white" alt="Documentation" align="center" />
    </a>
</p>

<p align="center"><img width=90% alt="" src="/media/tars-banner.png" /></p>

<p align="center">A recreation of the robot TARS from Interstellar, featuring AI capabilities.</p>

## Overview

TARS-AI is a physical robot recreation of TARS from the movie Interstellar, enhanced with modern AI capabilities. The system combines:

- **Natural Language Processing**: Conversational AI using large language models
- **Speech Recognition & Synthesis**: Voice interaction capabilities
- **Physical Movement**: Servo-controlled articulation
- **Computer Vision**: Image recognition and processing
- **Home Automation Integration**: Smart home control

## System Architecture

### Core Components

![System Architecture](/media/tars-ai.png)

1. **Main Application** (`app.py`): Central coordinator that initializes all modules and manages the system lifecycle.

2. **Module System**: Modular architecture with specialized components:
   - **Speech Processing**: STT (Speech-to-Text) and TTS (Text-to-Speech)
   - **Memory Management**: Short-term and long-term memory for contextual awareness
   - **Character System**: Personality traits and response generation
   - **Hardware Control**: Servo motor control for physical movement
   - **AI Engine**: Language model integration and inference

3. **Configuration System**: Settings management through:
   - `config.ini`: Main configuration file
   - `persona.ini`: Character-specific settings
   - `.env`: Sensitive credentials and API keys

## Hardware Components

### Physical Structure
- 3D printed chassis and articulating components
- Raspberry Pi as the main computing unit
- PCA9685 PWM controller for servo management
- Multiple servo motors for movement control

### Servo Control
- Torso movement (height, rotation)
- Arm and hand articulation
- Precise timing for smooth motion

### Input/Output
- Microphone for audio input
- Speakers for audio output
- Optional display for visual feedback
- Bluetooth controller support

## Software Components

### Speech Processing
- **STT Options**: Whisper, Vosk, Silero, or external API
- **TTS Options**: Piper, ElevenLabs, Azure, Silero, or espeak
- Wake word detection for activation

### AI Capabilities
- LLM integration (OpenAI, local models)
- Context-aware responses
- Memory management for conversation history
- Computer vision for image understanding

### Integrations
- Discord bot functionality
- Home Assistant integration
- Web interface for control and monitoring

## Installation

### Requirements
- Raspberry Pi 4 (recommended)
- Python 3.8+
- System dependencies:
  - Chromium browser
  - Audio processing tools (sox, portaudio)
  - Text-to-speech engine (espeak-ng)

### Quick Start
1. Clone the repository:
   ```bash
   git clone https://github.com/pyrater/TARS-AI.git
   cd TARS-AI
   ```

2. Run the installation script:
   ```bash
   ./Install.sh
   ```

3. Configure the system:
   - Edit `src/config.ini` with your settings
   - Create `.env` file with API keys

4. Start the system:
   ```bash
   cd src
   source .venv/bin/activate
   python app.py
   ```

## Configuration

The `config.ini` file contains all system settings, organized into sections:

- **[CONTROLS]**: Hardware and movement settings
- **[STT]**: Speech-to-text configuration
- **[CHAR]**: Character-specific settings
- **[LLM]**: Language model configuration
- **[TTS]**: Text-to-speech settings
- **[VISION]**: Computer vision settings
- **[SERVO]**: Servo control parameters

## Troubleshooting

### Common Issues

1. **Hardware Connection Problems**
   - Verify I2C device presence (`i2cdetect -y 1`)
   - Check servo connections and power supply

2. **API Key Errors**
   - Ensure correct keys in `.env`
   - Verify API service availability

3. **Audio Processing Issues**
   - Check audio device configuration
   - Verify required codecs are installed

## License & Attribution

TARS-AI is licensed under the [CC-BY-NC License](./LICENSE).

Please review the [Attribution Guidelines](./ATTRIBUTION.md) when using or modifying this project.

## Contributing

- See our contributing guidelines: [docs-tars-ai.vercel.app/contribute](https://docs-tars-ai.vercel.app/contribute)
- Join our Discord server: [discord.gg/AmE2Gv9EUt](https://discord.gg/AmE2Gv9EUt)