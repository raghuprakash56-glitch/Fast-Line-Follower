# Troubleshooting Guide

## Common Issues and Solutions

### 1. Arduino IDE Issues

#### Problem: Port Not Detected
**Symptoms**: COM port not appearing in Tools → Port menu

**Solutions**:
1. Reinstall CH340 driver (Windows) or FTDI drivers
2. Try different USB cable
3. Try different USB port on computer
4. Restart computer and IDE

#### Problem: Upload Fails with "avrdude: stk500_recv()"
**Symptoms**: Upload error after selecting board and port

**Solutions**:
1. Select correct board (Arduino Uno)
2. Select correct COM port
3. Close Serial Monitor before uploading
4. Try lower baud rate
5. Update Arduino IDE to latest version

---

### 2. Sensor Issues

#### Problem: Sensors Not Reading Values
**Symptoms**: Serial Monitor shows same value or 0/1023 always

**Solutions**:
1. Check power connections to sensors (5V and GND)
2. Verify analog pin connections (A0, A1, etc.)
3. Test with multimeter to check voltage output
4. Run sensor test code: `sensor_test.ino`
5. Check for loose jumper wires

**Diagnostic Code**:
```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  int sensor1 = analogRead(A0);
  int sensor2 = analogRead(A1);
  Serial.print("S1: "); Serial.print(sensor1);
  Serial.print(" S2: "); Serial.println(sensor2);
  delay(500);
}
```

#### Problem: Sensor Values Too Low/High
**Symptoms**: Readings always near 0 or always near 1023

**Solutions**:
1. Check sensor orientation (should face ground)
2. Adjust sensor height (2-3 cm from surface)
3. Check for dirt or debris on sensor lens
4. Verify power supply voltage to sensor
5. Try different IR sensors

#### Problem: Sensor Values Not Changing
**Symptoms**: Same value regardless of surface color

**Solutions**:
1. Re-calibrate sensors
2. Check sensor power connections
3. Move sensor closer/farther from surface
4. Adjust ambient lighting
5. Clean sensor lens with dry cloth

---

### 3. Motor Issues

#### Problem: Motors Not Running
**Symptoms**: No rotation despite code and power connections

**Solutions**:
1. Check battery power (test with multimeter)
2. Verify motor driver power connections
3. Check motor wiring (swap if needed)
4. Test motor directly with battery
5. Check for blown fuses on motor driver

**Diagnostic Code**:
```cpp
// Test motor on D8, D9
void setup() {
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
}

void loop() {
  digitalWrite(8, HIGH);
  digitalWrite(9, LOW);
  delay(2000);
  digitalWrite(8, LOW);
  digitalWrite(9, HIGH);
  delay(2000);
  digitalWrite(8, LOW);
  digitalWrite(9, LOW);
  delay(2000);
}
```

#### Problem: One Motor Runs, Other Doesn't
**Symptoms**: Only left or only right motor rotates

**Solutions**:
1. Check connections for non-functional motor
2. Swap motor connections on driver to test
3. Test motor directly with battery
4. Check motor driver output pins
5. Verify PWM pin connections

#### Problem: Motors Run Too Fast/Slow
**Symptoms**: Speed not matching expected PWM value

**Solutions**:
1. Adjust PWM value (0-255 range)
2. Check battery voltage (should be 6-12V)
3. Ensure motor driver has proper power supply
4. Check for motor overload (wheels stuck)
5. Balance PWM values for both motors

---

### 4. Line Following Issues

#### Problem: Robot Doesn't Follow Line
**Symptoms**: Robot moves in straight line or random direction

**Solutions**:
1. **Recalibrate sensors**: Run sensor calibration code
2. **Check line contrast**: Use black line on white surface
3. **Adjust threshold**: Try different threshold values
4. **Reduce speed**: Lower PWM value for better control
5. **Check motor balance**: Ensure equal motor speeds
6. **Verify control logic**: Review decision-making code

#### Problem: Robot Oscillates (Zigzag Motion)
**Symptoms**: Robot weaves left and right excessively

**Solutions**:
1. **Reduce speed**: Lower PWM value
2. **Increase threshold tolerance**: Add dead zone in code
3. **Implement PID control**: Use proportional control
4. **Increase sensor-to-motor delay**: Use `delay(100)`
5. **Check wheel alignment**: Ensure parallel alignment

#### Problem: Robot Loses Line on Curves
**Symptoms**: Robot goes off track at turns

**Solutions**:
1. **Reduce speed**: Slower speed for better tracking
2. **Widen turn radius**: Design wider curves
3. **Add more sensors**: Use 3+ sensors for better curve detection
4. **Implement lookahead logic**: Predict curve direction
5. **Adjust sensor position**: Move sensors further forward

#### Problem: Robot Follows Line Only When Slow
**Symptoms**: Good at low speed, loses track at high speed

**Solutions**:
1. **Reduce PWM incrementally**: Find sweet spot speed
2. **Increase sensor reading frequency**: Reduce delay
3. **Implement speed compensation**: Adjust control based on speed
4. **Use PID control**: Proportional-Integral-Derivative control
5. **Check sensor refresh rate**: Faster ADC sampling

---

### 5. Power Issues

#### Problem: Battery Drains Quickly
**Symptoms**: System stops working within minutes

**Solutions**:
1. Check for short circuits
2. Use battery with higher capacity
3. Reduce motor speed to lower current draw
4. Check for motor stalling or jamming
5. Upgrade to better battery (Li-Po recommended)

#### Problem: Voltage Drop Under Load
**Symptoms**: Arduino resets or sensors malfunction when motors run

**Solutions**:
1. Use separate power supplies for Arduino and motors
2. Add capacitors (1000µF) across power lines
3. Verify motor driver power supply rating
4. Check battery internal resistance
5. Upgrade to higher capacity battery

---

### 6. Circuit Connection Issues

#### Problem: Intermittent Behavior
**Symptoms**: Works sometimes, fails randomly

**Solutions**:
1. Check all wire connections (use multimeter)
2. Reseat all jumper wires
3. Check for corrosion on breadboard
4. Use better quality jumper wires
5. Avoid crossing power and signal wires

#### Problem: Ground Loop Issues
**Symptoms**: Erratic sensor readings or noisy output

**Solutions**:
1. Ensure common ground for all components
2. Use star grounding (single point)
3. Add decoupling capacitors (0.1µF) near chips
4. Keep signal wires away from power lines
5. Shield analog signal wires if needed

---

## Testing Checklist

Before troubleshooting further, verify:

- [ ] Arduino IDE recognizes COM port
- [ ] USB cable can upload code
- [ ] Battery has power (>6V measured)
- [ ] All connections are secure
- [ ] Sensors output values change
- [ ] Motors rotate when commanded
- [ ] Control logic is correct
- [ ] Line is high contrast (black/white)

---

## Advanced Diagnostics

### Using Serial Monitor for Debugging

```cpp
void setup() {
  Serial.begin(9600);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
}

void loop() {
  int s1 = analogRead(A0);
  int s2 = analogRead(A1);
  
  Serial.print("Sensor1: ");
  Serial.print(s1);
  Serial.print(" | Sensor2: ");
  Serial.print(s2);
  Serial.print(" | Threshold: 525");
  Serial.println();
  
  delay(500);
}
```

### Using Multimeter for Testing
1. **Voltage check**: Test power supply at various points
2. **Continuity test**: Verify wire connections
3. **Resistance test**: Check for short circuits
4. **Current draw**: Measure motor current

---

## Still Not Working?

If issues persist:
1. Create GitHub issue with detailed description
2. Provide error messages and serial output
3. Share code snippet causing problems
4. Include hardware configuration details
5. Provide photos of circuit connections

---

*Last Updated: June 2026*
*For additional help, check GitHub Issues or documentation*
