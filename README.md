# Fast Line Follower Robot

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Arduino](https://img.shields.io/badge/Platform-Arduino-00979D?logo=arduino)](https://www.arduino.cc/)

> A comprehensive learning repository for building intelligent line-following robots using Arduino microcontrollers and embedded systems.

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Quick Start](#quick-start)
- [Documentation](#documentation)
- [Learning Concepts](#learning-concepts)
- [Hardware Requirements](#hardware-requirements)
- [Contributing](#contributing)
- [License](#license)

## Overview

This repository documents a complete learning journey in robotics and embedded systems. It provides:

- **Practical implementations** of line-following algorithms
- **Hardware configuration guides** with circuit diagrams
- **Reusable code modules** for sensor and motor control
- **Educational documentation** for beginners and advanced users
- **Troubleshooting guides** for common issues

**Instructor:** Dr. Daniel Raj A  
**Platform:** [Etalvis.com](https://www.etalvis.com)

## 🎯 Key Features

✅ IR sensor-based line detection  
✅ PWM-based motor speed control  
✅ Modular, well-commented code  
✅ Comprehensive hardware documentation  
✅ PID control optimization ready  
✅ Production-ready circuit designs  

## 🛠 Technology Stack

| Component | Details |
|-----------|----------|
| **Language** | Embedded C / Arduino |  
| **Microcontroller** | Arduino Nano / Arduino Uno |
| **Sensors** | IR Sensors (TCRT5000) |
| **Motor Driver** | TB6612FNG |
| **Motors** | DC Motors with Encoders |
| **IDE** | Arduino IDE |

## 📁 Repository Structure

```
Fast-Line-Follower/
├── src/                           # Source code
│   ├── arduino/                   # Arduino sketches
│   │   ├── line_follower.ino      # Main implementation
│   │   ├── sensor_test.ino        # Sensor validation
│   │   └── motor_control.ino      # Motor control utilities
│   ├── embedded_c/                # Embedded C implementations
│   │   ├── main.c                 # Main program
│   │   ├── sensor.h/.c            # Sensor driver
│   │   └── motor_driver.h/.c      # Motor driver functions
│   └── utilities/                 # Helper libraries
│       ├── ir_sensor.h            # IR sensor handling
│       └── motor.h                # Motor control
│
├── hardware/                      # Hardware documentation
│   ├── arduino/                   # Arduino board info
│   │   ├── ARDUINO_NANO.md        # Nano specifications
│   │   ├── ARDUINO_PIN_CONFIG.md  # Pin configuration
│   │   └── images/
│   │       └── arduino_board.png
│   ├── motor_driver/              # Motor driver documentation
│   │   ├── TB6612FNG.md           # TB6612FNG datasheet info
│   │   ├── pin_connections.md     # Pin connection guide
│   │   └── images/
│   │       ├── tb6612fng.png
│   │       └── pin_config.png
│   └── encoder/                   # Encoder motor documentation
│       ├── ENCODER_MOTOR.md       # Encoder specifications
│       ├── pin_config.md          # Pin configuration
│       └── images/
│           └── encoder_motor.png
│
├── docs/                          # Documentation
│   ├── SETUP_GUIDE.md             # Getting started
│   ├── ARCHITECTURE.md            # System architecture
│   ├── TROUBLESHOOTING.md         # Common issues & solutions
│   ├── CALIBRATION.md             # Sensor calibration guide
│   └── CONCEPTS.md                # Learning concepts
│
├── tests/                         # Test files
│   ├── sensor_test/               # Sensor testing sketches
│   ├── motor_test/                # Motor testing sketches
│   └── integration_test/          # Full system tests
│
├── examples/                      # Example implementations
│   ├── basic_line_follow.ino      # Basic implementation
│   ├── advanced_pid_control.ino   # PID-based control
│   └── obstacle_detection.ino     # Enhanced algorithm
│
├── README.md                      # Main documentation
├── CHANGELOG.md                   # Version history
├── CONTRIBUTING.md                # Contribution guidelines
├── CODE_OF_CONDUCT.md             # Community standards
├── LICENSE                        # MIT License
└── .gitignore                     # Git ignore rules
```

## 🚀 Quick Start

### Prerequisites

- Arduino IDE (v1.8.19 or later)
- Arduino Nano/Uno microcontroller
- Required hardware components
- USB cable for programming

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/raghuprakash56-glitch/Fast-Line-Follower.git
   cd Fast-Line-Follower
   ```

2. **Set up hardware:**
   - Follow guides in `hardware/` directory
   - Connect sensors and motors according to pin configurations
   - Verify all connections

3. **Upload code:**
   ```bash
   # Open Arduino IDE
   # Load: src/arduino/line_follower.ino
   # Select Board: Arduino Nano
   # Select Port: COM3 (or your port)
   # Click Upload
   ```

4. **Test the robot:**
   ```bash
   # See docs/SETUP_GUIDE.md for detailed testing procedures
   ```

## 📚 Documentation

| Document | Purpose |
|----------|----------|
| [SETUP_GUIDE.md](docs/SETUP_GUIDE.md) | Hardware setup and configuration |
| [ARCHITECTURE.md](docs/ARCHITECTURE.md) | System design and control flow |
| [TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md) | Common issues and solutions |
| [CALIBRATION.md](docs/CALIBRATION.md) | Sensor calibration procedures |

## 🎓 Learning Concepts

This repository covers:

- **Robotics Fundamentals**
  - Line detection algorithms
  - Path following logic
  - Real-time control systems

- **Embedded Systems**
  - Microcontroller programming (Arduino/8051)
  - Digital input/output handling
  - PWM signal generation
  - Serial communication

- **Electronics**
  - Circuit design and connections
  - Motor control and drivers
  - Sensor interfacing
  - Power management

- **Advanced Topics**
  - PID control implementation
  - Obstacle detection
  - Speed optimization
  - Sensor fusion techniques

## 🔧 Hardware Requirements

| Component | Model | Purpose |
|-----------|-------|----------|
| Microcontroller | Arduino Nano | Main controller |
| Sensors | TCRT5000 (x2) | Line detection |
| Motor Driver | TB6612FNG | Motor control |
| Motors | DC Motors | Propulsion |
| Encoders | Optical Encoders | Speed feedback |
| Power | 9V Battery | Energy source |

## 📖 How to Use This Repository

### For Beginners
1. Read [SETUP_GUIDE.md](docs/SETUP_GUIDE.md)
2. Follow hardware connection guides in `hardware/`
3. Study `src/arduino/line_follower.ino`
4. Run test sketches from `tests/`

### For Developers
1. Review [ARCHITECTURE.md](docs/ARCHITECTURE.md)
2. Explore modular code in `src/utilities/`
3. Check `examples/` for advanced implementations
4. Refer to [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for:

- Code style guidelines
- Pull request process
- Bug reporting procedures
- Feature suggestions

## 📋 Code of Conduct

Please review [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) for community guidelines.

## 📝 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## 👨‍💼 Author

**Raghu Prakash C**

This repository represents a continuous learning journey in robotics and embedded systems, developed through hands-on experience and structured guidance from professional instructors.

## 🔗 Related Resources

- [Arduino Official Documentation](https://www.arduino.cc/)
- [Embedded Systems Guide](https://www.embedded.com/)
- [Robotics Learning Path](https://www.etalvis.com)

---

**Last Updated:** July 2026  
**Status:** Active Development  
**Issues:** [Open Issues](https://github.com/raghuprakash56-glitch/Fast-Line-Follower/issues)
