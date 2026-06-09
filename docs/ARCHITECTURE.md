# System Architecture

## Overview
The Line Follower Robot operates on a simple but effective control architecture that processes sensor input and generates motor control signals in real-time.

## System Block Diagram

```
┌─────────────┐
│  IR Sensors │ (Analog Input)
└──────┬──────┘
       │
       ▼
┌─────────────────────┐
│  Microcontroller    │ (ADC + Processing)
│  (Arduino/8051)     │
└──────┬──────────────┘
       │
       ▼
┌──────────────────┐
│  Motor Driver    │ (PWM Output)
│  (L293D/L298N)   │
└──────┬───────────┘
       │
       ▼
┌──────────────────┐
│   DC Motors      │
│  (Speed & Dir)   │
└──────────────────┘
```

## Control Flow

1. **Sensor Reading**: IR sensors detect line position
2. **ADC Conversion**: Analog values converted to digital
3. **Decision Logic**: Microcontroller determines required motor action
4. **PWM Generation**: Motor speed controlled via PWM signals
5. **Motor Response**: Motors adjust speed and direction

## Key Components

### Sensors (Input)
- IR sensors mounted on robot front
- Detect contrast between black line and white surface
- Output analog voltage (0-5V)

### Processor (Control)
- Microcontroller reads sensor values via ADC
- Runs decision-making algorithm
- Outputs PWM signals to motor driver

### Actuators (Output)
- Motor driver receives PWM signals
- Amplifies signals to drive motors
- Motors propel robot in desired direction

## Control Algorithm

```
WHILE robot is powered:
    1. Read IR sensor values
    2. Compare values against threshold
    3. Determine position relative to line
    4. Calculate motor speed adjustments
    5. Send PWM commands to motors
    6. Repeat
END
```

## Power Distribution

- **Sensor Power**: 5V (from Arduino)
- **Microcontroller**: 5V
- **Motor Supply**: 6-12V (battery)
- **Motor Driver**: 5V logic, 6-12V motor supply

---

*For implementation details, see relevant code files in src/ directory*
