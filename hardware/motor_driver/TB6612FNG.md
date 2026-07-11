# TB6612FNG Dual Motor Driver Documentation

## Overview

The TB6612FNG is a compact, dual motor driver IC capable of driving two DC motors in both forward and reverse directions. Perfect for robotics applications.

## Key Features

- ✅ Dual motor control
- ✅ Forward and reverse operation
- ✅ PWM speed control
- ✅ Low standby current
- ✅ Thermal shutdown protection
- ✅ Output short-circuit detection
- ✅ Small footprint (8-pin IC)

## Specifications

| Parameter | Value |
|-----------|-------|
| Supply Voltage (VM) | 4.5V - 13.5V |
| Logic Voltage (VCC) | 2.7V - 5.5V |
| Continuous Current (per motor) | 1.2A (typical) |
| Peak Current | 2A |
| Standby Current | 0.1µA |
| Operating Temperature | -20°C to +85°C |
| Package | 8-pin SOP |

## Pinout

```
        ┌─────────┐
PWMA    │ 1     8 │ PWMB
AIN1    │ 2     7 │ BIN1
AIN2    │ 3     6 │ BIN2
GND     │ 4     5 │ VM
        └─────────┘
```

### Pin Descriptions

| Pin | Name | Function | Type | Notes |
|-----|------|----------|------|-------|
| 1 | PWMA | Motor A speed control | Input | 0-5V PWM |
| 2 | AIN1 | Motor A direction bit 1 | Input | Digital |
| 3 | AIN2 | Motor A direction bit 2 | Input | Digital |
| 4 | GND | Ground | Ground | Common ground |
| 5 | VM | Motor power supply | Power | 4.5-13.5V |
| 6 | BIN2 | Motor B direction bit 2 | Input | Digital |
| 7 | BIN1 | Motor B direction bit 1 | Input | Digital |
| 8 | PWMB | Motor B speed control | Input | 0-5V PWM |

## Motor Control Truth Table

### Motor A (Using AIN1, AIN2, PWMA)

| AIN1 | AIN2 | PWMA | Action |
|------|------|------|--------|
| HIGH | LOW | 0-255 | Forward (speed controlled) |
| LOW | HIGH | 0-255 | Reverse (speed controlled) |
| HIGH | HIGH | Any | Brake (fast stop) |
| LOW | LOW | Any | Brake (free stop) |
| Any | Any | 0 | Standby (no movement) |

### Motor B (Using BIN1, BIN2, PWMB)

| BIN1 | BIN2 | PWMB | Action |
|------|------|------|--------|
| HIGH | LOW | 0-255 | Forward (speed controlled) |
| LOW | HIGH | 0-255 | Reverse (speed controlled) |
| HIGH | HIGH | Any | Brake (fast stop) |
| LOW | LOW | Any | Brake (free stop) |
| Any | Any | 0 | Standby (no movement) |

## Connection Diagram

```
                    TB6612FNG Motor Driver
                    ┌─────────────────┐
Arduino D8 ────────┤ PWMA         VM │────── +12V Motor Supply
Arduino D9 ────────┤ AIN1        BIN1│──────── Arduino D11
Arduino D10 ───────┤ AIN2        BIN2│──────── Arduino D12
Arduino GND ───────┤ GND         PWM │──────── Arduino D6
                    │              B │
Motor A+ ──────────┤ OUT-A     OUT-B │──────── Motor B+
Motor A- ──────────┤ OUT-A'    OUT-B'│──────── Motor B-
                    └─────────────────┘
                              │
                    Battery GND (Common)
```

## Arduino Connection Guide

### Hardware Setup

```cpp
// Motor A (Left Motor)
const int MOTOR_A_IN1 = 9;    // Direction control
const int MOTOR_A_IN2 = 10;   // Direction control
const int MOTOR_A_PWM = 5;    // Speed control (PWM pin)

// Motor B (Right Motor)
const int MOTOR_B_IN1 = 11;   // Direction control
const int MOTOR_B_IN2 = 12;   // Direction control
const int MOTOR_B_PWM = 6;    // Speed control (PWM pin)
```

### Code Example

```cpp
#include <Arduino.h>

// Motor A pins
const int MOTOR_A_IN1 = 9;
const int MOTOR_A_IN2 = 10;
const int MOTOR_A_PWM = 5;

// Motor B pins
const int MOTOR_B_IN1 = 11;
const int MOTOR_B_IN2 = 12;
const int MOTOR_B_PWM = 6;

void setup() {
  pinMode(MOTOR_A_IN1, OUTPUT);
  pinMode(MOTOR_A_IN2, OUTPUT);
  pinMode(MOTOR_A_PWM, OUTPUT);
  
  pinMode(MOTOR_B_IN1, OUTPUT);
  pinMode(MOTOR_B_IN2, OUTPUT);
  pinMode(MOTOR_B_PWM, OUTPUT);
}

// Motor A forward
void motorAForward(int speed) {
  digitalWrite(MOTOR_A_IN1, HIGH);
  digitalWrite(MOTOR_A_IN2, LOW);
  analogWrite(MOTOR_A_PWM, speed);  // 0-255
}

// Motor A reverse
void motorAReverse(int speed) {
  digitalWrite(MOTOR_A_IN1, LOW);
  digitalWrite(MOTOR_A_IN2, HIGH);
  analogWrite(MOTOR_A_PWM, speed);  // 0-255
}

// Motor A stop
void motorAStop() {
  digitalWrite(MOTOR_A_IN1, HIGH);
  digitalWrite(MOTOR_A_IN2, HIGH);
  analogWrite(MOTOR_A_PWM, 255);
}

// Similar functions for Motor B...

void loop() {
  // Example: Run motor forward at 75% speed
  motorAForward(192);  // 192/255 ≈ 75%
  delay(2000);
  
  motorAStop();
  delay(500);
  
  motorAReverse(192);
  delay(2000);
}
```

## Power Supply Recommendations

### Battery Selection
- **Voltage:** 6V-12V recommended (optimal: 9V or 12V)
- **Capacity:** 1000mAh minimum for continuous operation
- **Type:** LiPo, NiMH, or alkaline batteries

### Wiring Guidelines

1. **Separate Power Supplies:** Use separate batteries for logic (5V) and motors (9-12V)
2. **Common Ground:** Always connect GND of Arduino, driver, and battery
3. **Decoupling Capacitors:** 100µF electrolytic + 100nF ceramic near motor supply
4. **Wire Gauge:** Use 18-20 AWG for motor power lines
5. **Short Paths:** Keep motor connections as short as possible

## Performance Considerations

### Speed Control
- PWM frequency: 490 Hz (Arduino default)
- Resolution: 8-bit (0-255 values)
- Minimum speed for motor startup: ~100 (depending on motor)

### Current Limiting
- Peak current: 2A per motor
- Continuous: 1.2A per motor
- Use current limiting if driving heavy loads

### Thermal Management
- Chip operates up to 85°C
- Add heatsink if sustained high current
- Thermal shutdown activates if overheated

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| Motor won't move | Wrong pin configuration | Verify pin numbers and connections |
| Motor moves slowly | Low battery voltage | Check battery voltage (should be >6V) |
| Motor jerks | PWM frequency too low | Increase PWM value gradually |
| One motor stronger | Pin resistance difference | Check all connections for corrosion |
| Chip gets hot | High current draw | Check motor specifications, reduce load |

## Datasheets & References

- [TB6612FNG Datasheet (Toshiba)](https://www.sparkfun.com/datasheets/IC/Motor/TB6612FNG.pdf)
- [TB6612FNG Hookup Guide](https://learn.sparkfun.com/tutorials/tb6612fng-hookup-guide)

---

*Last Updated: July 2026*
