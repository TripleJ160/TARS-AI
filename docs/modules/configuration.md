# Configuration Module (module_config.py)

## Overview
The configuration module provides centralized management of system settings and environment variables.

## Key Features
1. **Configuration Loading**
   - Load from config.ini
   - Environment variable support
   - Default values

2. **Validation**
   - Required settings
   - Value ranges
   - Type checking

3. **Access Control**
   - Read-only access
   - Secure credential handling
   - Environment variable masking

## Code Structure
```python
@dataclass
class TTSConfig:
    def __getitem__(self, key):
    def validate(self) -> bool:
    @classmethod
    def from_config_dict(cls, config_dict: dict) -> 'TTSConfig':

def load_config():
def get_api_key(llm_backend: str) -> str:
def update_character_setting(setting, value):
```

## Configuration Sections
| Section | Purpose |
|---------|---------|
| CONTROLS | Hardware and movement settings |
| STT | Speech-to-text configuration |
| CHAR | Character-specific settings |
| LLM | Language model configuration |
| TTS | Text-to-speech settings |
| VISION | Computer vision settings |
| SERVO | Servo control parameters |

## Error Handling
- Missing configuration files
- Invalid values
- Environment variable errors
- Type conversion failures

## Integration Points
- All system modules
- Main application
- Hardware interfaces
- Web interface

## Security Considerations
- Credential management
- Environment variable handling
- Configuration file permissions
- Sensitive data masking