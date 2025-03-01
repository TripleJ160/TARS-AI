# Servo Tester (app-servotester.py)

## Overview
The servo tester provides tools for calibrating and testing servo motors used in TARS-AI's physical movement system.

## Key Features
1. **Manual Control**
   - Individual servo control
   - Pulse width adjustment
   - Real-time feedback

2. **Auto-Calibration**
   - Automatic range detection
   - Neutral position calculation
   - Safety checks

3. **Preset Management**
   - Predefined positions
   - Configuration saving
   - Quick testing

## Code Structure
```python
# Hardware initialization
pwm = Adafruit_PCA9685.PCA9685(busnum=1)
pwm.set_pwm_freq(60)

# Control functions
def set_servo_pulse(channel, pulse):
def auto_calibrate_servo(channel, is_center_servo=False):
def set_all_servos_preset():
```

## Calibration Process
1. **Minimum Pulse Detection**
   - Start from maximum pulse
   - Decrease until movement detected
   - Fine-tune with binary search

2. **Maximum Pulse Detection**
   - Start from minimum pulse
   - Increase until movement stops
   - Fine-tune with binary search

3. **Neutral Position Calculation**
   - Average of min/max pulses
   - Additional calculations for center servos

## Safety Features
- Pulse range validation
- Channel restrictions
- User confirmation prompts
- Emergency stop capability

## Integration Points
- Hardware control module
- Configuration system
- Movement system

## Usage Patterns
1. Initial hardware setup
2. Periodic recalibration
3. Troubleshooting
4. Development testing