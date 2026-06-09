# Setup and Installation Guide

## Prerequisites

### Hardware
- Arduino nano microcontroller board
- 2x IR sensors (TCRT5000 or similar)
- 2x DC motors (3-6V)
- Motor driver module (L293D or L298N)
- Battery pack (6-9V recommended)
- Robot chassis/frame
- Breadboard and jumper wires

### Software
- Arduino IDE v1.8.0 or higher
- USB cable for Arduino programming
- Text editor (optional, for code review)

---

## Step 1: Hardware Assembly

### Circuit Connections

#### IR Sensor Connections
```
TCRT5000 Sensor 1        Arduino
├─ VCC ────────────────→ 5V
├─ GND ────────────────→ GND
└─ OUT ────────────────→ A0 (Analog Pin)

TCRT5000 Sensor 2        Arduino
├─ VCC ────────────────→ 5V
├─ GND ────────────────→ GND
└─ OUT ────────────────→ A1 (Analog Pin)
```

#### Motor Driver (L293D) Connections
```
L293D Module             Arduino
├─ IN1 ─────────────────→ D8
├─ IN2 ─────────────────→ D9
├─ IN3 ─────────────────→ D10
├─ IN4 ─────────────────→ D11
├─ GND ─────────────────→ GND
└─ +12V (Motor Supply)   Battery (+)

Motors to L293D:
├─ Motor 1 OUT1 & OUT2
└─ Motor 2 OUT3 & OUT4
```

#### Power Distribution
```
Battery (6-9V)
├─ (+) → Motor Driver +12V, Arduino Vin
└─ (-) → GND (common ground for all components)
```

### Physical Placement
1. **Sensors**: Mount IR sensors at 45° angle, 2-3 cm above ground
2. **Motors**: Attach to rear wheels
3. **Motor Driver**: Place on robot chassis
4. **Arduino**: Secure in center of chassis
5. **Battery**: Mount for optimal weight distribution

---

## Step 2: Software Installation

### Install Arduino IDE
1. Visit [arduino.cc/software](https://www.arduino.cc/en/software)
2. Download for your operating system (Windows/Mac/Linux)
3. Run installer and complete setup

### Connect Arduino to Computer
1. Plug USB cable from Arduino to computer
2. Open Device Manager (Windows) or System Report (Mac)
3. Note the COM port (e.g., COM3, COM4)

---

## Step 3: Sensor Calibration

### Calibration Process
1. Open `src/arduino/sensor_calibration.ino` in Arduino IDE
2. Upload to Arduino board
3. Open Serial Monitor (Baud: 9600)
4. Place robot on **white surface** and note readings
5. Place robot on **black line** and note readings
6. Calculate threshold: `(white_value + black_value) / 2`

### Example Output
```
White surface reading: 850
Black line reading: 200
Calculated threshold: 525
```

### Update Main Code
Update the threshold value in your main code:
```cpp
#define THRESHOLD 525
```

---

## Step 4: Motor Testing

### Upload Motor Test Code
1. Open `src/arduino/motor_test.ino`
2. Upload to Arduino
3. Both motors should rotate forward for 2 seconds, then backward

### Troubleshooting Motor Issues
- **No rotation**: Check battery power and connections
- **One motor not rotating**: Check motor driver connections
- **Erratic movement**: Check for loose connections

---

## Step 5: Upload Main Code

### Basic Implementation
1. Open `src/arduino/basic_line_follower.ino`
2. Select board: **Tools → Board → Arduino Uno**
3. Select port: **Tools → Port → COM[your_port]**
4. Click **Upload**

### Monitor Behavior
1. Place robot on floor with black line
2. Power on battery
3. Robot should follow the line
4. Open Serial Monitor to view sensor values in real-time

---

## Troubleshooting

### Arduino Won't Upload
- Check USB cable connection
- Try different USB port
- Restart Arduino IDE
- Verify correct board selected

### Sensors Not Reading
- Check wiring connections
- Verify sensor power (use multimeter)
- Check Arduino ADC pins
- Test with `sensor_test.ino`

### Robot Not Following Line
- Calibrate sensors again
- Check motor connections
- Verify PWM output (D9, D10 for L293D)
- Slow down PWM value for better control
- Check physical alignment of sensors

### Erratic Behavior
- Clean sensor lenses
- Reduce PWM speed for stability
- Add capacitors to sensor output for filtering
- Check for loose connections

---

## Performance Optimization

### Tips for Better Line Following
1. **Sensor Placement**: Position sensors close to line
2. **Lighting**: Use consistent lighting conditions
3. **Surface**: Use high-contrast black line on white surface
4. **Speed**: Start slow (PWM ~150), increase gradually
5. **Motor Balance**: Ensure both motors have equal power

---

## Next Steps

- Review advanced implementations in `src/arduino/advanced_control.ino`
- Implement PID control for smoother tracking
- Add obstacle detection
- Experiment with speed optimization

---

*Last Updated: June 2026*
