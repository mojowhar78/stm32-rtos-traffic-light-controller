# STM32 FreeRTOS Traffic Light Controller

A multitasking traffic light control system implemented on an STM32F103 microcontroller using FreeRTOS kernel. The system is fully simulated in Proteus 8 Professional for real-time testing and validation.

## 📋 Overview

This project demonstrates advanced embedded systems concepts including real-time multitasking, inter-task communication, GPIO control, and UART debugging on a microcontroller. The traffic light follows a standard cycle: RED → YELLOW → GREEN → YELLOW → RED.

### Key Features

- **Multitasking Architecture**: Three independent FreeRTOS tasks for concurrent execution
- **Safe Inter-task Communication**: FreeRTOS message queues for reliable state transitions
- **Real-time LED Control**: GPIO-based light control with immediate response to state changes
- **UART Monitoring**: Real-time status output for debugging and system observation
- **Priority-based Scheduling**: Configured task priorities for deterministic behavior
- **Hardware Simulation**: Complete Proteus 8 Professional simulation environment

## 🔧 System Architecture

### Task Structure

#### 1. **Controller Task** (Highest Priority)
- Manages state machine logic
- Implements RED → YELLOW → GREEN → YELLOW cycle
- Sends state transitions via message queue to LED Task
- Timing control for each traffic light phase

#### 2. **LED Task** (Medium Priority)
- Receives state commands from Controller Task via queue
- Updates GPIO pins to control physical LEDs
- Ensures immediate visual feedback on state changes
- Prevents race conditions through queue-based communication

#### 3. **Monitor Task** (Lower Priority)
- Receives state updates from Controller Task
- Outputs current state via UART for real-time monitoring
- Provides debugging information and system status
- Non-blocking UART communication
