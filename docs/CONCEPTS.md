# Learning Concepts - Fast Line Follower Robot

## Table of Contents
1. [Robotics Fundamentals](#robotics-fundamentals)
2. [Embedded Systems](#embedded-systems)
3. [Electronics & Circuits](#electronics--circuits)
4. [Control Systems](#control-systems)
5. [Advanced Topics](#advanced-topics)

---

## Robotics Fundamentals

### Line Detection

**Concept:** The robot uses IR sensors to detect black lines on white surfaces (or vice versa).

**How it works:**
1. IR LED emits infrared light
2. Light reflects off the surface
3. Photodiode receives reflected light
4. Output voltage varies with surface color
5. Microcontroller reads analog value

**Key Points:**
- White surfaces reflect more IR light (higher readings)
- Black surfaces absorb IR light (lower readings)
- Calibration determines the threshold between values

### Path Following Algorithm

**Bang-Bang Control:**
```
IF (left_sensor > threshold AND right_sensor < threshold)
    Move RIGHT
ELSE IF (left_sensor < threshold AND right_sensor > threshold)
    Move LEFT
ELSE IF (both_sensors > threshold)
    Move FORWARD
ELSE
    Stop / Search
```

**Advantages:** Simple, fast, easy to implement
**Disadvantages:** Not smooth, may oscillate, poor curve tracking

### Logic Building

**Key Decision Points:**
- Sensor readings interpretation
- Motor speed adjustment
- Error detection and handling
- Edge case management

---

## Embedded Systems

### Microcontroller Programming

**Arduino Platform:**
- Simplified C/C++ environment
- Built-in libraries for I/O
- Serial communication capabilities
- PWM generation
- Analog-to-digital conversion

**Key Functions:**
```cpp
setup()          // Runs once at startup
loop()           // Runs repeatedly
analogRead()     // Read analog pin (0-1023)
digitalRead()    // Read digital pin (HIGH/LOW)
analogWrite()    // PWM output (0-255)
digitalWrite()   // Digital output (HIGH/LOW)
```

### Digital I/O Handling

**Input Types:**
- Analog input from sensors (A0-A7 on Nano)
- Digital input from buttons/encoders
- Serial input from host computer

**Output Types:**
- PWM output to motor controllers
- Digital output to LEDs/relays
- Serial output for debugging

### PWM (Pulse Width Modulation)

**What it is:** Variable duty cycle digital signal

**Formula:**
```
Duty Cycle (%) = (ON_time / Period) × 100
Average Voltage = Max_Voltage × (Duty_Cycle / 100)
```

**Usage in Robots:**
- Motor speed control (0-255 maps to 0-5V)
- LED brightness control
- Servo motor positioning

---

## Electronics & Circuits

### Motor Driver (TB6612FNG)

**Purpose:** Amplify microcontroller signals to drive motors

**Key Connections:**
```
Arduino → TB6612FNG → Motor
```

**Pin Functions:**
| Pin | Function |
|-----|----------|
| IN1, IN2 | Direction control |
| PWM | Speed control |
| OUT1, OUT2 | Motor outputs |
| GND | Ground reference |

**Motor Control Truth Table:**
| IN1 | IN2 | Action |
|-----|-----|--------|
| HIGH | LOW | Forward |
| LOW | HIGH | Backward |
| HIGH | HIGH | Stop (Brake) |
| LOW | LOW | Stop (Free) |

### IR Sensor Circuit

**Components:**
- IR LED (emitter)
- Photodiode (receiver)
- Resistor (load/pull-up)
- Capacitor (noise filtering)

**Signal Path:**
```
Reflected Light → Photodiode → Voltage Change → ADC → Digital Value
```

### Power Management

**Voltage Requirements:**
- Microcontroller: 5V
- IR Sensors: 5V
- Motors: 6-12V (typical)
- Motor Driver: 4.5-13.5V

**Power Distribution:**
- Use voltage regulator for stable 5V to logic circuits
- Keep motor power separate (heavy current draws)
- Include capacitors for noise filtering

---

## Control Systems

### Proportional-Integral-Derivative (PID) Control

**Why PID?**
- Bang-bang control is jerky and inefficient
- PID provides smooth, proportional response
- Better curve tracking and stability

**Components:**

1. **Proportional (P):** Response proportional to error
   ```
   Output = Kp × Error
   ```

2. **Integral (I):** Accumulates past errors
   ```
   Output = Ki × Σ(Error)
   ```

3. **Derivative (D):** Responds to rate of change
   ```
   Output = Kd × (dError/dt)
   ```

**Combined PID Formula:**
```cpp
error = desired - actual
P_out = Kp * error
I_out = Ki * integral_of_error
D_out = Kd * rate_of_error_change
Output = P_out + I_out + D_out
```

**Tuning Guide:**
- **Increase Kp:** Faster response, but risk oscillation
- **Increase Ki:** Handles steady-state error, but slow
- **Increase Kd:** Reduces overshoot, improves stability

### Sensor Calibration

**Why calibrate?**
- Sensor readings vary with ambient light
- Different surfaces reflect different amounts
- Consistent calibration ensures reliable operation

**Calibration Steps:**
1. Place sensor on white surface, record value
2. Place sensor on black surface, record value
3. Calculate threshold: (white_value + black_value) / 2
4. Store calibration values

---

## Advanced Topics

### Obstacle Detection

**Ultrasonic Sensor Approach:**
- Send pulse, measure echo time
- Distance = (echo_time × speed_of_sound) / 2
- Stop or turn if obstacle detected

### Path Memory

**Concept:** Remember the path and optimize future traversals

**Implementation:**
- Store turn sequences in EEPROM
- Replay with optimized speeds
- Detect and handle dynamic obstacles

### Sensor Fusion

**Combine multiple sensor inputs:**
- IR sensors: Line detection
- Encoders: Distance/speed verification
- Accelerometer: Acceleration detection
- Gyroscope: Orientation tracking

### Wireless Control

**Bluetooth Integration:**
- HC-05 Bluetooth module
- Smartphone app control
- Real-time parameter tuning
- Data logging to cloud

---

## Practice Exercises

1. **Sensor Reading:** Read and log IR sensor values
2. **Motor Testing:** Test forward, backward, turn movements
3. **Calibration:** Properly calibrate sensors for your environment
4. **Line Following:** Implement basic bang-bang algorithm
5. **PID Tuning:** Implement and tune PID controller
6. **Obstacle Avoidance:** Add obstacle detection
7. **Performance Measurement:** Measure speed, accuracy, power consumption

---

For more information, see [ARCHITECTURE.md](ARCHITECTURE.md) and [TROUBLESHOOTING.md](TROUBLESHOOTING.md).
