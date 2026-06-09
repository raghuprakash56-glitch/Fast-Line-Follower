# Contributing to Fast Line Follower Robot

Thank you for your interest in contributing to this project! Contributions of all kinds are welcome, including code improvements, bug reports, documentation, and examples.

## Code of Conduct

- Be respectful and constructive
- Provide helpful feedback
- Respect different experience levels
- Focus on the code, not the person

## How to Contribute

### 1. Report Bugs

Create an issue with:
- Clear title describing the problem
- Detailed description of the issue
- Steps to reproduce
- Expected vs. actual behavior
- Hardware and software details
- Serial output or error messages

**Example**:
```
Title: Sensors not reading values with Arduino Uno

Description:
When I run sensor_test.ino, the Serial Monitor shows 0 for both sensors
regardless of surface color.

Steps to Reproduce:
1. Connect two TCRT5000 sensors to A0 and A1
2. Upload sensor_test.ino
3. Open Serial Monitor at 9600 baud

Expected: Values change between ~200-1000 based on surface
Actual: Always shows 0

Hardware: Arduino Uno, TCRT5000 sensors
Arduino IDE: v1.8.19
```

### 2. Suggest Features

Create an issue with:
- Clear description of the feature
- Use case and benefits
- Possible implementation approach
- Any relevant references

**Example**:
```
Title: Add PID control for smoother line following

Description:
Current implementation uses bang-bang control. PID would provide smoother
motor speed adjustments and better curve tracking.

Implementation could use:
- Proportional term for current error
- Integral term for error history
- Derivative term for rate of change
```

### 3. Submit Code Changes

#### Step 1: Fork the Repository
```bash
# Click "Fork" on GitHub
git clone https://github.com/YOUR-USERNAME/Fast-Line-Follower.git
cd Fast-Line-Follower
```

#### Step 2: Create a Feature Branch
```bash
git checkout -b feature/descriptive-name
# Example: git checkout -b feature/add-pid-control
```

#### Step 3: Make Changes
- Follow existing code style and formatting
- Add comments for complex logic
- Update documentation if needed
- Test thoroughly

#### Step 4: Commit with Clear Messages
```bash
git add .
git commit -m "Add PID control for smooth line following

- Implement P, I, D terms
- Tune constants for optimal performance
- Add calibration guide
- Test on various track widths"
```

#### Step 5: Push and Create Pull Request
```bash
git push origin feature/descriptive-name
# Then click "New Pull Request" on GitHub
```

### 4. Improve Documentation

Documentation improvements are highly valued:
- Fix typos or unclear explanations
- Add diagrams or examples
- Expand troubleshooting section
- Create tutorials

## Coding Standards

### Style Guidelines

```cpp
// Use meaningful variable names
int sensorLeftValue = analogRead(A0);  // Good
int s1 = analogRead(A0);               // Avoid

// Add comments for complex logic
if (sensorDifference > THRESHOLD) {
    // Adjust motor speed based on error magnitude
    motorSpeed = baseSpeed + (sensorDifference * CORRECTION_FACTOR);
}

// Use constants for magic numbers
#define THRESHOLD 525
#define MAX_PWM 255
#define MIN_PWM 0

// Consistent indentation (2 or 4 spaces)
void loop() {
  readSensors();
  calculateMotorSpeed();
  updateMotors();
}
```

### File Organization

```
src/
├── arduino/
│   ├── feature_name.ino          # Main implementation
│   ├── feature_name_test.ino     # Unit tests
│   └── README.md                 # Feature documentation
├── embedded_c/
│   ├── main.c
│   └── utilities.h
└── utilities/
    ├── sensor_handler.h
    └── motor_driver.h
```

### Documentation

- Use clear, concise language
- Include code examples
- Provide troubleshooting tips
- Link to relevant resources

## Pull Request Process

1. **Describe your changes**: What, why, and how
2. **Reference issues**: Link to related issues with `#123`
3. **Test thoroughly**: Ensure no regressions
4. **Update docs**: If applicable
5. **Keep it focused**: One feature/fix per PR
6. **Respond to feedback**: Be open to suggestions

### PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement

## Testing
- [ ] Tested on Arduino Uno
- [ ] Tested on [specific hardware]
- [ ] No regressions observed

## Checklist
- [ ] Code follows style guidelines
- [ ] Comments added for complex logic
- [ ] Documentation updated
- [ ] Tested in real hardware
```

## Contribution Ideas

### Easy (Good for beginners)
- [ ] Add code comments
- [ ] Improve documentation
- [ ] Create usage examples
- [ ] Fix typos
- [ ] Add sensor calibration tips

### Medium
- [ ] Implement obstacle detection
- [ ] Add Bluetooth control
- [ ] Optimize motor control
- [ ] Create test suite
- [ ] Add new features

### Challenging
- [ ] Implement PID control
- [ ] Add machine learning integration
- [ ] Create wireless control system
- [ ] Optimize power consumption
- [ ] Implement path memorization

## Questions?

- Check existing issues and pull requests
- Review documentation
- Ask in a new issue
- Comment on related discussions

## Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Credited in commit history
- Mentioned in release notes

---

**Thank you for contributing!** Your efforts help make this project better for everyone.

*Last Updated: June 2026*
