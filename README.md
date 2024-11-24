# ICS-3203-CAT2-Assembly-Mchory-Aroun-Mbashu-135448-
**Assembly language CAT 2-**

# 1. Control Flow and Conditional Logic

# Number Classifier

This project classifies input numbers as positive, negative, or zero using assembly language. Below are the jump instructions used, their impact on program flow, and build/run instructions.


## Build and Run Instructions



```
# Assemble for 64-bit
nasm -f elf64 number_classifier.asm -o number_classifier.o

# Link for 64-bit
ld -o number_classifier number_classifier.o

# Make executable
chmod +x number_classifier

# Run
./number_classifier
```
#  2. Array Manipulation with Looping and Reversal

Array Reversal Program (64-bit).
Purpose: Accepts 5 integers, reverses them in place, and displays the result

## Build and Run Instructions


```
# Assemble
nasm -f elf64 array_reversal.asm -o array_reversal.o

# Link
ld -o array_reversal array_reversal.o

# Make executable
chmod +x array_reversal

# Run
./array_reversal
```

## memory-related challenges
1. Input Storage Challenge:
    - Need to handle ASCII input but store as numbers
    - Solution: Convert ASCII to numeric during input
    - Impact: Requires careful handling of ASCII/numeric conversion

 2. In-Place Reversal Challenge:
    - Must swap values without using additional array
    - Solution: Use registers as temporary storage
    - Impact: Minimizes memory usage but requires careful register management

 3. Array Bounds Challenge:
    - Must track array boundaries during reversal
    - Solution: Use two indices (left/right) moving toward center
    - Impact: Prevents out-of-bounds access and ensures complete reversal

 4. Memory Access Patterns:
    - Direct memory access for array elements
    - Byte-level operations for single-digit numbers
    - Register-based temporary storage for swaps

 5. Memory Efficiency:
    - No additional array allocation
    - Minimal temporary storage
    - Direct manipulation of original array

 # 3. Modular Program with Subroutines for Factorial Calculation
 
  Factorial Calculator Program (64-bit)
  
Purpose: Calculate factorial using subroutines and stack management

 Features: Proper register preservation, modular design, stack usage

 ** STACK MANAGEMENT DOCUMENTATION **
 
Stack Operations Details:

 1. Main Program Stack Usage:
    - Preserves input number before factorial calculation
    - Maintains 16-byte alignment for system calls

 2. Factorial Subroutine Stack Frame:
    - Creates standard stack frame with base pointer
    - Preserves RCX for loop counter
    - Preserves RDI containing input number
    - Restores in reverse order (LIFO)

 3. Number Conversion Stack Usage:
    - Temporarily stores digits during conversion
    - Preserves registers for string manipulation
    - Maintains proper alignment throughout

 4. Stack Frame Management:
    - Each subroutine establishes its own frame
    - Properly deallocates all stack space
    - Ensures no stack leaks or corruption

  ## Build and Run Instructions

```
# Assemble
nasm -f elf64 factorial.asm -o factorial.o

# Link
ld -o factorial factorial.o

# Make executable
chmod +x factorial

# Run
./factorial
```

# 4.Data Monitoring and Control Using Port-Based Simulation

# Water Level Control System Documentation

 Water Level Control System Simulation
 
 Purpose: Monitor water level and control motor/alarm accordingly
 
 Simulates reading from sensors and controlling output devices

## 1. Memory Location Usage

### Sensor Input Simulation
- **`sensor_value`**: Single byte memory location storing the current water level (0-99).
- Input is simulated through user input.

### Control Outputs
- **`motor_status`**: Single byte representing motor state (`1=ON`, `0=OFF`).
- **`alarm_status`**: Single byte representing alarm state (`1=ON`, `0=OFF`).

---

## 2. Decision Logic

### Threshold Values
- **LOW_THRESHOLD**: 30 (minimum acceptable water level).
- **HIGH_THRESHOLD**: 80 (maximum acceptable water level).

### Control Logic Flow
1. **Low Water Level** (≤ 30):
   - **Motor**: ON (fills tank).
   - **Alarm**: OFF.
   - **Action**: Begin filling the tank.

2. **Normal Water Level** (31-79):
   - **Motor**: OFF.
   - **Alarm**: OFF.
   - **Action**: Monitor only.

3. **High Water Level** (≥ 80):
   - **Motor**: OFF (prevent overflow).
   - **Alarm**: ON (alert operator).
   - **Action**: Emergency response needed.

---

## 3. Program Structure

### Main Components
1. **`read_sensor`**:
   - Simulates sensor reading.
   - Currently uses keyboard input.
   - Stores value in `sensor_value`.

2. **`process_sensor_data`**:
   - Implements control logic.
   - Compares sensor value against thresholds.
   - Sets appropriate motor and alarm states.
   - Uses separate memory locations for device status.

3. **`update_outputs`**:
   - Handles device control.
   - Updates motor and alarm based on status flags.
   - Currently displays status messages.

---

## 4. Port/Memory Manipulation

### Current Implementation
- Uses memory locations to simulate I/O ports.
- Easily modifiable for real hardware by replacing memory references with port I/O instructions.



