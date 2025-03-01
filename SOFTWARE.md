# TARS-AI Software Documentation

This document provides detailed information about the software components, configuration, and customization options for TARS-AI.

## Software Architecture

TARS-AI follows a modular architecture with the following key components:

1. **Core Application** (`app.py`): Main entry point and coordinator
2. **Module System**: Specialized components for different functionalities
3. **Configuration System**: Settings management and validation
4. **Web Interface**: User interaction and control

## Installation

### Prerequisites
- Raspberry Pi OS (Bullseye or newer)
- Python 3.8+
- Git

### Installation Steps

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
   - Copy `src/config.ini.template` to `src/config.ini`
   - Copy `.env.template` to `.env`
   - Edit both files with your settings

4. Start the system:
   ```bash
   cd src
   source .venv/bin/activate
   python app.py
   ```

## Configuration

### config.ini

The main configuration file is divided into sections:

#### [CONTROLS]
```ini
controller_name = 8BitDo  # Name of the Bluetooth controller
enabled = False           # Enable controller support
voicemovement = False     # Enable voice-controlled movement
```

#### [STT] (Speech-to-Text)
```ini
wake_word = hey tar       # Wake word for activation
sensitivity = 8           # Wake word sensitivity (1-10)
stt_processor = faster-whisper  # STT engine (faster-whisper, vosk, silero, external)
whisper_model = tiny      # Whisper model size (tiny, base, small, medium, large)
vosk_model = vosk-model-small-en-us-0.15  # Vosk model name
use_indicators = True     # Use audio indicators when listening
vad_method = rms          # Voice activity detection method (rms, silero)
```

#### [CHAR] (Character)
```ini
character_card_path = character/TARS/TARS.json  # Character definition
user_name = Joe           # User's name
user_details = Species: Human. Gender: Male.  # User details for context
```

#### [LLM] (Language Model)
```ini
llm_backend = openai      # LLM provider (openai, tabby, ooba)
base_url = https://api.openai.com  # API endpoint
openai_model = gpt-4o-mini  # Model name
contextsize = 4000        # Maximum context size
max_tokens = 1000         # Maximum response tokens
temperature = 0.8         # Response randomness (0-1)
```

#### [TTS] (Text-to-Speech)
```ini
ttsoption = piper         # TTS engine (piper, silero, espeak, azure, elevenlabs, alltalk)
ttsurl = http://192.168.2.57:7852  # URL for external TTS server
toggle_charvoice = True   # Use character-specific voice
tts_voice = en-US-Steffan:DragonHDLatestNeural  # Voice name
```

### Environment Variables (.env)

Sensitive credentials are stored in the `.env` file:

```
OPENAI_API_KEY=your_openai_key_here
ELEVENLABS_API_KEY=your_elevenlabs_key_here
AZURE_API_KEY=your_azure_key_here
DISCORD_TOKEN=your_discord_token_here
HA_TOKEN=your_home_assistant_token_here
```

## Module System

### Speech Processing

#### Speech-to-Text (STT)
TARS-AI supports multiple STT engines:

1. **Faster Whisper**
   - High accuracy, GPU acceleration
   - Configure in `config.ini`:
     ```ini
     stt_processor = faster-whisper
     whisper_model = tiny  # Options: tiny, base, small, medium, large
     ```

2. **Vosk**
   - Offline capability, lower resource usage
   - Configure in `config.ini`:
     ```ini
     stt_processor = vosk
     vosk_model = vosk-model-small-en-us-0.15
     ```

3. **Silero**
   - Lightweight, good for low-resource systems
   - Configure in `config.ini`:
     ```ini
     stt_processor = silero
     ```

4. **External Server**
   - Use a separate server for STT processing
   - Configure in `config.ini`:
     ```ini
     stt_processor = external
     external_url = http://your-server:port
     ```

#### Text-to-Speech (TTS)
TARS-AI supports multiple TTS engines:

1. **Piper**
   - Local TTS with voice cloning
   - Configure in `config.ini`:
     ```ini
     ttsoption = piper
     ```

2. **ElevenLabs**
   - High-quality cloud TTS
   - Configure in `config.ini` and `.env`:
     ```ini
     ttsoption = elevenlabs
     voice_id = JBFqnCBsd6RMkjVDRZzb
     model_id = eleven_multilingual_v2
     ```
     ```
     ELEVENLABS_API_KEY=your_key_here
     ```

3. **Azure**
   - Enterprise-grade cloud TTS
   - Configure in `config.ini` and `.env`:
     ```ini
     ttsoption = azure
     azure_region = eastus
     tts_voice = en-US-Steffan:DragonHDLatestNeural
     ```
     ```
     AZURE_API_KEY=your_key_here
     ```

4. **Silero**
   - Lightweight local TTS
   - Configure in `config.ini`:
     ```ini
     ttsoption = silero
     ```

5. **espeak**
   - Basic local TTS
   - Configure in `config.ini`:
     ```ini
     ttsoption = espeak
     ```

### Memory System

The memory system manages conversation context and persistent knowledge:

1. **Short-term Memory**
   - Stores recent conversation turns
   - Provides context for responses
   - Automatically managed

2. **Long-term Memory**
   - Stores persistent knowledge
   - Retrieves relevant information based on context
   - Configure in `config.ini`:
     ```ini
     [RAG]
     strategy = hybrid  # Options: naive, hybrid
     top_k = 5          # Number of memories to retrieve
     ```

### Character System

The character system manages personality and response generation:

1. **Character Definition**
   - JSON file with character attributes
   - Located in `character/[NAME]/[NAME].json`

2. **Personality Traits**
   - Defined in `character/[NAME]/persona.ini`
   - Influence response style and behavior

## Web Interface

TARS-AI includes a web-based interface for interaction:

1. **Enable the Interface**
   - Configure in `config.ini`:
     ```ini
     [CHATUI]
     enabled = True
     ```

2. **Access the Interface**
   - Open a browser to `http://[raspberry-pi-ip]:5012`

3. **Features**
   - Text chat interface
   - Voice interaction
   - System status monitoring

## Integration Options

### Discord Bot

TARS-AI can function as a Discord bot:

1. **Enable Discord Integration**
   - Configure in `config.ini` and `.env`:
     ```ini
     [DISCORD]
     enabled = True
     channel_id = your_channel_id
     ```
     ```
     DISCORD_TOKEN=your_discord_token
     ```

2. **Invite the Bot**
   - Create a Discord application at https://discord.com/developers/applications
   - Generate a bot token and add to `.env`
   - Invite the bot to your server

### Home Assistant

TARS-AI can integrate with Home Assistant:

1. **Enable Home Assistant Integration**
   - Configure in `config.ini` and `.env`:
     ```ini
     [HOME_ASSISTANT]
     enabled = True
     url = http://your-home-assistant:8123
     ```
     ```
     HA_TOKEN=your_home_assistant_token
     ```

2. **Usage**
   - Control smart home devices through voice commands
   - Get status updates from Home Assistant

## Customization

### Adding New TTS Voices

1. **For Piper**:
   - Download voice models from https://github.com/rhasspy/piper/releases
   - Place in `src/tts/` directory
   - Update `config.ini`:
     ```ini
     ttsoption = piper
     tts_voice = your_new_voice
     ```

### Adding New Characters

1. **Create Character Directory**:
   ```bash
   mkdir -p src/character/NEW_CHARACTER
   ```

2. **Create Character JSON**:
   ```bash
   touch src/character/NEW_CHARACTER/NEW_CHARACTER.json
   ```
   
3. **Create Persona INI**:
   ```bash
   touch src/character/NEW_CHARACTER/persona.ini
   ```

4. **Edit Character JSON**:
   ```json
   {
     "char_name": "New Character",
     "char_greeting": "Hello, I am New Character!",
     "char_persona": "I am a helpful assistant with a friendly personality.",
     "example_dialogue": [
       {"user": "Hello there!", "char": "Hi! How can I help you today?"},
       {"user": "What can you do?", "char": "I can assist with various tasks, answer questions, and have conversations."}
     ]
   }
   ```

5. **Edit Persona INI**:
   ```ini
   [PERSONA]
   humor = 7
   creativity = 8
   knowledge = 9
   helpfulness = 10
   ```

6. **Update Configuration**:
   ```ini
   [CHAR]
   character_card_path = character/NEW_CHARACTER/NEW_CHARACTER.json
   ```

## Troubleshooting

### Common Software Issues

1. **Module Import Errors**
   - Ensure virtual environment is activated
   - Reinstall dependencies: `pip install -r requirements.txt`

2. **API Connection Errors**
   - Verify API keys in `.env`
   - Check internet connection
   - Confirm API service status

3. **Audio Device Issues**
   - List audio devices: `arecord -l` and `aplay -l`
   - Set default devices in `~/.asoundrc`
   - Check microphone permissions