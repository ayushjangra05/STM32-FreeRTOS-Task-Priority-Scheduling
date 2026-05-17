# STM32-FreeRTOS-Task-Priority-Scheduling
FreeRTOS-based multitasking project on STM32F446RE demonstrating task creation, priority-based scheduling, LED control, and SWV ITM trace debugging using CMSIS-RTOS V2 and STM32CubeIDE.

## Overview

This project demonstrates how FreeRTOS manages multiple tasks with different priority levels using preemptive scheduling.

Two independent tasks are created to:

- Toggle LEDs periodically
- Print task execution messages to the SWV ITM console
- Observe the effect of task priorities on CPU scheduling

The project is developed using:

- STM32CubeMX
- STM32CubeIDE
- FreeRTOS Middleware
- CMSIS-RTOS V2 API

---

## Features

- FreeRTOS task creation
- Priority-based preemptive scheduling
- Dual LED control using separate tasks
- SWV ITM trace debugging
- CMSIS-RTOS V2 implementation
- Real-time task monitoring

---

## Hardware Requirements

- STM32 Nucleo-F446RE Development Board
- LEDs
- Breadboard
- Resistors
- Connecting Wires
- USB Type-A to Mini-B Cable

---

## Software Requirements

- STM32CubeIDE
- STM32CubeMX
- FreeRTOS Middleware

---

## Peripheral Configuration

| Peripheral | Configuration |
|------------|----------------|
| PA5 | GPIO Output (LED_1) |
| PA6 | GPIO Output (LED_2) |
| SYS Debug | Trace Asynchronous SW |
| Timebase Source | TIM6 |
| RTOS Interface | CMSIS_V2 |

---

## RTOS Task Configuration

| Task | Function | Priority |
|------|-----------|-----------|
| LED_1 | Toggle LED on PA5 | Configurable |
| LED_2 | Toggle LED on PA6 | Configurable |

Both tasks execute with:

```c
osDelay(500);
```

which creates periodic task execution every 500 ms.

---

## Working Principle

FreeRTOS uses preemptive scheduling where higher-priority tasks receive CPU access before lower-priority tasks.

The scheduler:

- Switches between tasks automatically
- Handles task delays using RTOS tick interrupts
- Allows multitasking without blocking the CPU

Task execution messages are monitored using the SWV ITM Data Console.

---

## Source Code

### Task 1

```c
void Task1_function(void *argument)
{
    for(;;)
    {
        HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);

        printf("Task_1 Executing for LED Toggle \n");

        osDelay(500);
    }
}
```

---

### Task 2

```c
void StartLED_2(void *argument)
{
    for(;;)
    {
        HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_6);

        printf("Task_2 Executing for LED Toggle \n");

        osDelay(500);
    }
}
```

---

## SWV ITM Trace Configuration

The SWV ITM console is used for real-time debugging and task tracing.

### Features

- Observe task execution
- Monitor scheduling behaviour
- View console messages without UART
- Analyze task timing

---

## Build and Run

1. Open the project in STM32CubeIDE
2. Configure FreeRTOS middleware
3. Build the project
4. Connect STM32 board via USB
5. Start debugging mode
6. Enable SWV ITM Data Console
7. Start trace and run the program

---

## Expected Output

- Both LEDs blink periodically
- SWV ITM console displays task execution logs
- Higher-priority tasks execute more frequently under CPU load
- Scheduling behaviour changes with task priorities

---

## Learning Outcomes

- Understanding FreeRTOS architecture
- Task creation and scheduling
- Priority-based multitasking
- SWV ITM debugging
- CMSIS-RTOS V2 API usage
- Real-time embedded system design

---

## Future Improvements

- Add mutex and semaphore synchronization
- Implement inter-task communication
- Add UART logging
- Create dynamic priority scheduling
- Integrate sensor-based RTOS tasks

---

## Author

**Ayush Jangra**  
ECE Student | Chitkara University
