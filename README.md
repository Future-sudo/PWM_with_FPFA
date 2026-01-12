# PWM_with_FPFA
📁 Project Structure
text
pwm-generator/
├── pwm.v              # Main PWM module
├── tb_pwm.v           # Test bench
├── README.md          # This file
└── .gitignore         # Git ignore file
🎯 Features
Configurable Resolution: Parameterized bit-width (default 4-bit = 16 levels)

Real-time Control: Increment/decrement duty cycle during operation

Debounced Inputs: Edge detection for reliable button presses

Full Range Coverage: 0% to 100% duty cycle

Reset Functionality: Synchronous reset for initialization

📊 Module Interface
verilog
module pwm #(parameter WIDTH = 4)(
    input  wire clk,    // Clock input
    input  wire rst,    // Active-high reset
    input  wire inc,    // Increment duty cycle
    input  wire dec,    // Decrement duty cycle
    output wire pwm     // PWM output signal
);
🔧 Parameters
Parameter	Default	Description
WIDTH	4	Bit-width of counter/duty cycle (resolution = 2^WIDTH levels)
🚀 How It Works
Counter: Free-running counter increments on every clock cycle

Duty Cycle Register: Stores current duty cycle value (0 to 2^WIDTH-1)

Comparator: Outputs HIGH when counter < duty_cycle

Control Logic:

inc button: Increases duty cycle (up to maximum)

dec button: Decreases duty cycle (down to zero)

Simultaneous press: No change (priority logic)

⚙️ Technical Details
Clock Domain: All logic synchronous to input clock

Input Debouncing: 2-stage synchronizer for inc/dec inputs

Pulse Detection: Rising-edge detection for control signals

Resolution: For WIDTH=4 → 16 steps (6.25% per step)

📈 Timing Characteristics
PWM frequency = Clock frequency / 2^WIDTH

Example: 100MHz clock, WIDTH=4 → PWM frequency = 6.25MHz

Duty cycle changes synchronous to clock edges
