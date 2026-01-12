Here's a comprehensive GitHub description for your PWM Generator project:

---

# PWM Generator - Verilog Implementation

A configurable Pulse Width Modulation (PWM) generator implemented in Verilog with adjustable duty cycle control. This module generates PWM signals with configurable resolution and provides user controls for incrementing/decrementing the duty cycle in real-time.

## 📁 Project Structure
```
pwm-generator/
├── pwm.v              # Main PWM module
├── tb_pwm.v           # Test bench
├── README.md          # This file
└── .gitignore         # Git ignore file
```

## 🎯 Features
- **Configurable Resolution**: Parameterized bit-width (default 4-bit = 16 levels)
- **Real-time Control**: Increment/decrement duty cycle during operation
- **Debounced Inputs**: Edge detection for reliable button presses
- **Full Range Coverage**: 0% to 100% duty cycle
- **Reset Functionality**: Synchronous reset for initialization

## 📊 Module Interface
```verilog
module pwm #(parameter WIDTH = 4)(
    input  wire clk,    // Clock input
    input  wire rst,    // Active-high reset
    input  wire inc,    // Increment duty cycle
    input  wire dec,    // Decrement duty cycle
    output wire pwm     // PWM output signal
);
```

## 🔧 Parameters
| Parameter | Default | Description |
|-----------|---------|-------------|
| `WIDTH` | 4 | Bit-width of counter/duty cycle (resolution = 2^WIDTH levels) |

## 🚀 How It Works
1. **Counter**: Free-running counter increments on every clock cycle
2. **Duty Cycle Register**: Stores current duty cycle value (0 to 2^WIDTH-1)
3. **Comparator**: Outputs HIGH when counter < duty_cycle
4. **Control Logic**: 
   - `inc` button: Increases duty cycle (up to maximum)
   - `dec` button: Decreases duty cycle (down to zero)
   - Simultaneous press: No change (priority logic)

## ⚙️ Technical Details
- **Clock Domain**: All logic synchronous to input clock
- **Input Debouncing**: 2-stage synchronizer for inc/dec inputs
- **Pulse Detection**: Rising-edge detection for control signals
- **Resolution**: For WIDTH=4 → 16 steps (6.25% per step)

## 📈 Timing Characteristics
- PWM frequency = Clock frequency / 2^WIDTH
- Example: 100MHz clock, WIDTH=4 → PWM frequency = 6.25MHz
- Duty cycle changes synchronous to clock edges

## 🧪 Simulation
```bash
# Compile
iverilog -o sim pwm.v tb_pwm.v

# Run simulation
vvp sim

# View waveforms (if using GTKWave)
gtkwave pwm_tb.vcd
```

## 🎛️ Example Usage
```verilog
// 8-bit resolution PWM (256 levels)
pwm #(.WIDTH(8)) pwm_inst (
    .clk(clk_100MHz),
    .rst(reset),
    .inc(button_up),
    .dec(button_down),
    .pwm(led_driver)
);
```

## 📋 Applications
- LED brightness control
- Motor speed regulation
- Power converters
- Audio signal generation
- DAC implementation

## 🔍 Design Considerations
- **Synchronization**: All inputs synchronized to avoid metastability
- **Boundary Protection**: Prevents overflow/underflow of duty cycle
- **Resource Efficient**: Minimal logic utilization
- **Scalable**: Easy to adjust resolution via parameter

## 📝 License
MIT License - See LICENSE file for details.

## 👨‍💻 Author
**Bhavishya Hardiya**  
*IIST (Indian Institute of Space Science and Technology)*

## 🔗 Related Projects
- [FPGA Boolean Board](https://github.com/boolean-board)
- [Verilog Tutorials](https://github.com/verilog-tutorials)

---

### Quick Start
1. Clone the repository
2. Simulate with your preferred Verilog simulator
3. Integrate into your FPGA project
4. Connect to physical buttons/LEDs for real-time control

---
*This project is part of the Boolean Board learning series for digital design and FPGA development.*
