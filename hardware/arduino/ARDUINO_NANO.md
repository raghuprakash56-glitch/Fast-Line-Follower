# Arduino Nano Board Documentation

## Overview

The Arduino Nano is a small, breadboard-friendly microcontroller board based on the ATmega328P processor.

## Specifications

| Parameter | Value |
|-----------|-------|
| Microcontroller | ATmega328P |
| Operating Voltage | 5V |
| Input Voltage (recommended) | 7-12V |
| Input Voltage (limits) | 6-20V |
| Digital I/O Pins | 14 (6 with PWM) |
| Analog Input Pins | 8 (A0-A7) |
| DC Current per I/O Pin | 40 mA |
| Flash Memory | 32 KB |
| SRAM | 2 KB |
| EEPROM | 1 KB |
| Clock Speed | 16 MHz |
| Dimensions | 18 × 45 mm |
| Weight | 7g |

## Pin Layout

```
                    ┌─────────┐
              Reset │ RST  5V │ Power
         TX (D1/1) │ TX   GND│ GND
         RX (D0/0) │ RX   D13│ D13 (LED)
        A0 (AREF)  │ AREF D12│ D12 (MISO)
        A1 (D15)   │ A0   D11│ D11 (MOSI/PWM)
        A2 (D16)   │ A1   D10│ D10 (SS/PWM)
        A3 (D17)   │ A2   D9 │ D9 (PWM)
        A4 (D18)   │ A3   D8 │ D8
        A5 (D19)   │ A4   D7 │ D7
        A6 (D20)   │ A5   D6 │ D6 (PWM)
        A7 (D21)   │ A6   D5 │ D5 (PWM)
         (GND)     │ A7   D4 │ D4
         (AREF)    │ GND  D3 │ D3 (PWM)
         (VCC)     │ REF  D2 │ D2
                    │     D1 │ D1 (TX)
                    │     D0 │ D0 (RX)
                    └─────────┘
```

## Pin Functions

### Analog Pins (A0-A7)
- 10-bit ADC resolution
- Range: 0-1023 (maps to 0-5V)
- Used for sensor inputs
- Can be used as digital I/O (D14-D21)

### PWM Pins (D3, D5, D6, D9, D10, D11)
- 8-bit PWM (0-255)
- 490 Hz frequency (default)
- Used for motor speed control

### Serial Communication Pins (D0-RX, D1-TX)
- 0-115200 baud rate (typically 9600)
- Used for debugging and communication

## Power Pins

| Pin | Function | Voltage |
|-----|----------|----------|
| 5V | Power Output | +5V |
| 3.3V | Power Output | +3.3V |
| GND | Ground | 0V |
| VIN | Power Input | 7-12V |
| RST | Reset | Active LOW |

## Communication Interfaces

### Serial (UART)
- Pins: D0 (RX), D1 (TX)
- Baud Rate: 9600 (default)
- Used for debugging via Serial Monitor

### SPI (Serial Peripheral Interface)
- MOSI: D11
- MISO: D12
- SCK: D13
- SS: D10

### I2C/TWI
- SDA: A4
- SCL: A5

## Application Notes

### For Line Follower Robot

**Recommended Pin Assignments:**

```cpp
// IR Sensors (Analog Input)
const int SENSOR_LEFT = A0;    // Left IR sensor
const int SENSOR_RIGHT = A1;   // Right IR sensor

// Motor Driver Control (Digital + PWM)
const int MOTOR_LEFT_DIR = 2;  // Direction control
const int MOTOR_LEFT_PWM = 3;  // Speed control (PWM)

const int MOTOR_RIGHT_DIR = 4; // Direction control
const int MOTOR_RIGHT_PWM = 5;  // Speed control (PWM)

// Encoder Inputs
const int ENCODER_LEFT = 6;    // Interrupt pin
const int ENCODER_RIGHT = 7;   // Interrupt pin

// Status LED
const int STATUS_LED = 13;     // Built-in LED
```

### Power Supply Considerations

1. **Voltage Regulation:** Use 7.5V input for optimal performance
2. **Decoupling Capacitor:** Add 100nF capacitor near power pins
3. **Heavy Current Loads:** Separate motor power supply
4. **Ground Connection:** Common ground between all components

### Limitations

- Limited RAM (2 KB) - watch array sizes
- Single ADC - use multiplexing for many sensors
- Limited drive current - use transistors for heavy loads
- No native USB - use FTDI chip for programming

## Programming

1. Connect via USB or FTDI adapter
2. Select "Arduino Nano" in Arduino IDE
3. Select correct COM port
4. Choose "ATmega328P" processor
5. Upload sketch

## Troubleshooting

- **No COM Port:** Install CH340 drivers or use FTDI adapter
- **Upload Fails:** Check processor and port selection
- **Erratic Behavior:** Verify power supply voltage (should be 5V)
- **Sensor Readings Off:** Add decoupling capacitors

## References

- [Arduino Nano Official Page](https://www.arduino.cc/en/Guide/ArduinoNano)
- [ATmega328P Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/ATmega48A-PA-88A-PA-168A-PA-328-P-DS-DS40002061B.pdf)

---

*Last Updated: July 2026*
