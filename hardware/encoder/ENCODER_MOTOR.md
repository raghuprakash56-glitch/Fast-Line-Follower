# Encoder Motor Documentation

## Overview

Encoder motors are DC motors equipped with integrated optical or magnetic encoders that provide feedback about motor shaft rotation, enabling speed measurement and position tracking.

## Key Features

- ✅ Speed feedback capability
- ✅ Position tracking
- ✅ Accurate motor control
- ✅ RPM measurement
- ✅ Distance calculation
- ✅ Synchronized dual-motor operation

## Specifications (Typical)

| Parameter | Value |
|-----------|-------|
| Motor Type | DC Brushed |
| Rated Voltage | 6V - 12V |
| Rated Speed | 100-300 RPM (geared) |
| Rated Torque | 0.5-2 Nm |
| Encoder Type | Optical |
| PPR (Pulses Per Revolution) | 20, 60, or 120 (depends on model) |
| Output Type | Open collector or push-pull |
| Number of Output Channels | 2 (A and B - quadrature) |

## Motor Connections

### Power Pins

| Pin | Function | Voltage |
|-----|----------|----------|
| Red | Motor Positive | +6 to +12V |
| Black | Motor Negative | Ground (0V) |

### Encoder Output Pins

| Pin | Function | Signal |
|-----|----------|--------|
| Yellow | Channel A | TTL / Open Collector |
| White | Channel B | TTL / Open Collector |
| Green | Ground | 0V |

## Encoder Fundamentals

### How Encoders Work

1. **Optical Disk:** Encoder disk attached to motor shaft with transparent and opaque slots
2. **Light Source:** LED emits light through disk
3. **Photodetector:** Receives reflected light pulses
4. **Signal Generation:** Creates digital pulses corresponding to shaft rotation

### Pulses Per Revolution (PPR)

```
Revolutions = Total Pulses / PPR
```

**Example (PPR = 20):**
- 20 pulses = 1 complete revolution
- 40 pulses = 2 complete revolutions
- 1 pulse = 18° rotation

### Quadrature Encoding (Channels A & B)

**Why Two Channels?**
- Determine rotation direction
- Double resolution (2 pulses per slot)
- Error detection

**Direction Detection:**

```
Clockwise:  A rises, then B rises
Counter-clockwise: B rises, then A rises
```

**Signal Pattern:**

```
Forward rotation:
A: ├─┤ ├─┤ ├─┤
B:   ├─┤ ├─┤ ├─┤
     ↑ ↑ ↑ ↑ ↑
     Direction change point

Reverse rotation:
A:   ├─┤ ├─┤ ├─┤
B: ├─┤ ├─┤ ├─┤
```

## Arduino Integration

### Pin Connection

```cpp
// Left Motor Encoder
const int ENCODER_LEFT_A = 2;   // Interrupt pin
const int ENCODER_LEFT_B = 4;   // Regular pin

// Right Motor Encoder  
const int ENCODER_RIGHT_A = 3;  // Interrupt pin
const int ENCODER_RIGHT_B = 7;  // Regular pin

// Motor Parameters
const int PPR = 20;             // Pulses per revolution
```

### Code Implementation

```cpp
// Global variables
volatile long encoderCountLeft = 0;
volatile long encoderCountRight = 0;

// Interrupt handler for left encoder
void handleLeftEncoderA() {
  if (digitalRead(ENCODER_LEFT_A) == digitalRead(ENCODER_LEFT_B)) {
    encoderCountLeft--;  // Reverse
  } else {
    encoderCountLeft++;  // Forward
  }
}

// Interrupt handler for right encoder
void handleRightEncoderA() {
  if (digitalRead(ENCODER_RIGHT_A) == digitalRead(ENCODER_RIGHT_B)) {
    encoderCountRight--;  // Reverse
  } else {
    encoderCountRight++;  // Forward
  }
}

void setup() {
  pinMode(ENCODER_LEFT_A, INPUT);
  pinMode(ENCODER_LEFT_B, INPUT);
  pinMode(ENCODER_RIGHT_A, INPUT);
  pinMode(ENCODER_RIGHT_B, INPUT);
  
  // Attach interrupts to rising edge
  attachInterrupt(digitalPinToInterrupt(ENCODER_LEFT_A), 
                  handleLeftEncoderA, RISING);
  attachInterrupt(digitalPinToInterrupt(ENCODER_RIGHT_A), 
                  handleRightEncoderA, RISING);
}

// Calculate revolutions
float getRevolutions(long count) {
  return (float)count / PPR;
}

// Calculate distance (wheel diameter in cm)
float getDistance(long count, float wheelDiameter) {
  float revolutions = getRevolutions(count);
  float circumference = 3.14159 * wheelDiameter;
  return revolutions * circumference;
}

// Calculate RPM
float getRPM(long count, unsigned long timeMs) {
  float revolutions = getRevolutions(count);
  float minutes = timeMs / 60000.0;
  return revolutions / minutes;
}
```

## Applications in Line Follower

### 1. Speed Measurement
```cpp
// Measure speed every 100ms
unsigned long lastTime = 0;
long lastCount = 0;

void loop() {
  unsigned long currentTime = millis();
  
  if (currentTime - lastTime >= 100) {
    long encoderDelta = encoderCountLeft - lastCount;
    float rpm = (encoderDelta * 60000.0) / (100 * PPR);
    
    Serial.print("RPM: ");
    Serial.println(rpm);
    
    lastCount = encoderCountLeft;
    lastTime = currentTime;
  }
}
```

### 2. Distance Measurement
```cpp
// Measure distance traveled
const float WHEEL_DIAMETER = 6.5;  // cm

float distanceTraveled() {
  return getDistance(encoderCountLeft, WHEEL_DIAMETER);
}
```

### 3. Motor Synchronization
```cpp
// Keep both motors at same speed
void synchronizeMotors() {
  int leftSpeed = 200;   // 0-255
  int rightSpeed = 200;
  
  // Calculate error
  int error = encoderCountLeft - encoderCountRight;
  
  // Adjust right motor to match left
  if (error > 0) {
    rightSpeed += 10;  // Speed up right motor
  } else if (error < 0) {
    rightSpeed -= 10;  // Slow down right motor
  }
  
  // Constrain to valid range
  rightSpeed = constrain(rightSpeed, 0, 255);
  
  // Apply speeds
  setMotorSpeed(MOTOR_LEFT, leftSpeed);
  setMotorSpeed(MOTOR_RIGHT, rightSpeed);
}
```

## Performance Tips

1. **Use Interrupts:** Don't poll encoder pins in main loop
2. **Fast Sampling:** Read encoder values frequently (at least 10x motor frequency)
3. **Filter Noise:** Add capacitors near encoder output lines
4. **Debounce:** Implement software debouncing if needed
5. **Calibrate PPR:** Verify actual PPR value for your motors

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| No encoder signal | Loose connection | Check all connections |
| Erratic readings | Noise interference | Add 100nF capacitors on signal lines |
| Wrong direction | Reversed B channel | Swap channels or flip motor polarity |
| Missed pulses | Interrupt handler too slow | Optimize code, increase sampling |
| One motor faster | Motor/encoder mismatch | Calibrate and synchronize motors |

## References

- [Quadrature Encoder Guide](https://www.pjrc.com/teensy/td_libs_Encoder.html)
- [Motor Encoder Circuit Design](https://www.instructables.com/Arduino-DC-Motor-Control/)

---

*Last Updated: July 2026*
