# FreeRTOS Traffic Light Controller — STM32F103

A multitasking traffic light control system built on STM32F103 
microcontroller using FreeRTOS real-time operating system, 
simulated in Proteus 8 Professional.

---

## Demo

![Circuit](Images/circuit.png)
![Simulation](Images/simulation.png)

---

## Project Overview

This project demonstrates core FreeRTOS concepts including:
- Multitasking with priority based scheduling
- Inter-task communication using message queues
- GPIO control for LED output
- UART transmission for real time monitoring

---

## System Architecture
```
Controller Task (High Priority)
        │
        ├──► lightQueue ──► LED Task (Normal Priority)
        │                   Controls PA0, PA1, PA2 GPIO pins
        │
        └──► monitorQueue ──► Monitor Task (Low Priority)
                              Sends UART status messages
```

### Task Details

| Task | Priority | Function |
|------|----------|----------|
| ControllerTask | High | Manages RED→YELLOW→GREEN→YELLOW cycle |
| LEDTask | Normal | Controls GPIO pins for LED output |
| MonitorTask | Low | Sends light status over UART |

---

## Traffic Light Timing

| State | Duration |
|-------|----------|
| RED | 10 seconds |
| YELLOW | 3 seconds |
| GREEN | 10 seconds |
| YELLOW | 3 seconds |

---

## Hardware

| Component | Value |
|-----------|-------|
| Microcontroller | STM32F103C6T6 |
| LED Resistors | 220 ohm |
| Supply Voltage | 3.3V |
| UART Baud Rate | 115200 |

### Pin Connections

| STM32 Pin | Component |
|-----------|-----------|
| PA0 | RED LED |
| PA1 | YELLOW LED |
| PA2 | GREEN LED |
| PA9 | UART TX → Virtual Terminal |

---

## Software Stack

| Tool | Version |
|------|---------|
| STM32CubeIDE | 1.13.2 |
| FreeRTOS | CMSIS_V2 |
| HAL Library | STM32F1xx |
| Proteus | 8 Professional |

---

## FreeRTOS Concepts Demonstrated

**Message Queues**
Two separate queues used for inter-task communication:
- `lightQueue` — carries state to LED Task
- `monitorQueue` — carries state to Monitor Task

This ensures each task independently receives state 
changes without shared variables or race conditions.

**Priority Scheduling**
Controller runs at highest priority ensuring precise 
timing. LED Task at normal priority for responsive 
GPIO control. Monitor Task at lowest priority for 
background UART logging.

**Task States**
Tasks block on queue receive using osWaitForever — 
consuming zero CPU while waiting. Instantly wake 
when data arrives.

---

## UART Output

Virtual Terminal shows real time light status:
```
LIGHT: RED is ON
LIGHT: YELLOW is ON
LIGHT: GREEN is ON
LIGHT: YELLOW is ON
LIGHT: RED is ON
```

---

## What I Learned

- FreeRTOS task creation and lifecycle management
- Inter-task communication using queues
- Priority based preemptive scheduling
- STM32 GPIO and UART peripheral configuration
- Difference between mutex, semaphore and queue
- Priority inversion and deadlock concepts
- Embedded system simulation in Proteus

---

## How to Run

### Proteus Simulation
1. Open `Proteus/traffic_signal.pdsprj`
2. Load hex file from `Debug/` folder into STM32
3. Set crystal frequency to 8MHz
4. Click Play

### Build from Source
1. Open project in STM32CubeIDE 1.13.2
2. Project → Build All
3. Hex file generated in `Debug/` folder

---

## Author

**Your Name**
Embedded Systems Learner
[LinkedIn](your-linkedin-url) | [GitHub](your-github-url)