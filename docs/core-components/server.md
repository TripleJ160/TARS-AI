# API Server (app-server.py)

## Overview
The API server provides REST endpoints for vision and audio processing capabilities. It runs as a separate Flask application within the main system.

## Key Features
1. **Image Processing**
   - BLIP model for image captioning
   - Image format handling
   - Error handling

2. **Audio Processing**
   - Whisper model for speech-to-text
   - Audio format conversion
   - Transcription management

## Endpoints
| Endpoint | Method | Description |
|----------|--------|-------------|
| /caption | POST | Generate caption for uploaded image |
| /save_audio | POST | Transcribe uploaded audio |

## Code Structure
```python
# Flask app initialization
app = Flask(__name__)
CORS(app)

# Model initialization
blip_processor, blip_model = initialize_blip_model()
whisper_model = initialize_whisper_model()
```

## Image Processing Flow
1. Receive image file
2. Validate and convert format
3. Process with BLIP model
4. Generate caption
5. Return JSON response

## Audio Processing Flow
1. Receive audio file
2. Validate format
3. Transcribe with Whisper
4. Format transcription
5. Return JSON response

## Error Handling
- Invalid file formats
- Model initialization errors
- Processing failures

## Integration Points
- Vision module
- Audio processing module
- Main application
- Configuration system

## Performance Considerations
- Model size selection
- Device optimization (CPU/GPU)
- Batch processing