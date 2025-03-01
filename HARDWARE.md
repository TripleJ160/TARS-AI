# TARS-AI Hardware Documentation

This document provides detailed information about the hardware components, assembly, and configuration for the TARS-AI robot.

## Components List

### Core Electronics
- Raspberry Pi 4 (4GB or 8GB RAM recommended)
- PCA9685 PWM Servo Controller
- Power supply (5V for Raspberry Pi, separate power for servos)
- Microphone (USB or I2S)
- Speaker (3.5mm or I2S)
- Optional: 3.5" or 5.0" LCD display

### Servo Motors
- 6 standard servos for main movements
- Additional servos for arm and hand articulation
- Recommended: MG996R or similar for torso, SG90 for smaller joints

### Structural Components
- 3D printed chassis and articulating parts (STL files in `/3d Printer Files/`)
- M3 screws and nuts
- Bearings for smooth movement
- Connecting rods and linkages

## Assembly Instructions

### 1. Chassis Assembly
- Print all required STL files from the `/3d Printer Files/A. Required/` directory
- Assemble the chassis components according to the design
- Install bearings in designated locations
- Secure with M3 screws

### 2. Electronics Installation
- Mount Raspberry Pi in the designated location in the chassis
- Connect PCA9685 to Raspberry Pi via I2C (pins 3 & 5)
- Install microphone and speaker
- Connect power supply

### 3. Servo Installation
- Install servos in their designated positions:
  - Center servo for height adjustment
  - Port and starboard servos for rotation
  - Arm servos for articulation
- Connect all servos to the PCA9685 controller

### 4. Wiring Diagram
```
Raspberry Pi GPIO Pins:
- Pin 3 (SDA) → PCA9685 SDA
- Pin 5 (SCL) → PCA9685 SCL
- 5V → PCA9685 VCC
- GND → PCA9685 GND

PCA9685 Servo Connections:
- Channel 0: Center lift servo
- Channel 1: Port drive servo
- Channel 2: Starboard drive servo
- Channel 3: Port main arm
- Channel 4: Port forearm
- Channel 5: Port hand
- Channel 6: Starboard main arm
- Channel 7: Starboard forearm
- Channel 8: Starboard hand
```

## Servo Configuration

### Default Servo Positions
These values can be adjusted in the `config.ini` file:

```ini
[SERVO]
# Center Lift Servo (0) Values
upHeight = 88
neutralHeight = 168
downHeight = 250

# Port Drive Servo (1) Values
forwardPort = 400
neutralPort = 350
backPort = 300
perfectportoffset = 0

# Starboard Drive Servo (2) Values
forwardStarboard = 300
neutralStarboard = 350
backStarboard = 400
perfectStaroffset = 0

# Arm Servo Values
portMain = 610
portForarm = 570
portHand = 570
starMain = 200
starForarm = 200
starHand = 240
```

### Servo Calibration
Use the `app-servotester.py` utility to calibrate servo positions:

1. Run the servo tester:
   ```bash
   cd src
   source .venv/bin/activate
   python app-servotester.py
   ```

2. Select option 6 to auto-calibrate a servo, or options 2-5 to manually set servo positions

3. Update the `config.ini` file with the calibrated values

## Display Options

### 3.5" LCD Display
- Print the files from `/3d Printer Files/B. 3.5Inch/`
- Connect the display to the Raspberry Pi
- Configure in `config.ini`:
  ```ini
  [CHATUI]
  enabled = True
  ```

### 5.0" LCD Display
- Print the files from `/3d Printer Files/B. 5.0Inch/`
- Connect the display to the Raspberry Pi
- Configure in `config.ini` as above

## Power Management

### Power Requirements
- Raspberry Pi: 5V, 3A power supply
- Servos: Separate 5-6V power supply capable of handling peak current
  - Recommended: 5V 10A power supply for all servos

### Power Connections
- Never connect servo power directly to Raspberry Pi
- Use separate power supplies for logic and servos
- Connect common ground between power supplies

## Troubleshooting

### Servo Issues
- **Jittering**: Check power supply capacity, use separate power for servos
- **Limited Range**: Adjust min/max values in config.ini
- **No Movement**: Verify connections to PCA9685, check servo power

### I2C Connection Issues
- Verify I2C is enabled: `sudo raspi-config` → Interfaces → I2C → Enable
- Check connections with `i2cdetect -y 1`
- Default PCA9685 address should be 0x40

### 3D Printing Tips
- Use at least 20% infill for structural parts
- Support material needed for overhangs
- PETG or ABS recommended for durability
- Layer height: 0.2mm for balance of detail and strength