# STM32 Ultrasonic Servo Scanner

Obstacle detection and distance measurement system using an **STM32 Nucleo-L152RE**, an **HC-SR04 ultrasonic sensor** and an **SG90 servomotor**.

The project supports both **manual** and **automatic** operation modes. In automatic mode, the servomotor performs a sweep across different angular positions and the ultrasonic sensor measures the distance to possible obstacles at each position.

## Overview

This project was developed using low-level STM32 programming, configuring peripherals directly through registers instead of relying on high-level HAL functions.

The system combines GPIO, timers, PWM, input capture, external interrupts, ADC and UART communication to implement a complete embedded application.

## Main Features

* Distance measurement using an HC-SR04 ultrasonic sensor
* Manual and automatic operation modes
* Servo motor sweep in automatic mode
* PWM generation for SG90 servo control
* Echo pulse measurement using timer input capture
* Distance indication using LEDs
* UART output for debugging and distance monitoring
* ADC reading for analog input control
* Button-based mode selection and manual measurement
* Interrupt-driven design

## Hardware

* STM32 Nucleo-L152RE
* HC-SR04 ultrasonic distance sensor
* SG90 servomotor
* LEDs
* Push buttons
* Analog input connected to ADC
* UART connection through USART2

## Pin Configuration

| Function              | Pin             |
| --------------------- | --------------- |
| Ultrasonic Trigger    | PC8             |
| Ultrasonic Echo       | PC9             |
| Distance LEDs         | PC0 - PC4       |
| Measurement LED       | PB5             |
| Manual Measure Button | PB4             |
| Mode Button           | PC13            |
| Mode LED              | PA5             |
| ADC Input             | PA1             |
| Servo PWM             | PA0             |
| UART                  | USART2          |

## Operation Modes

### Manual Mode

In manual mode, the user presses the measurement button to trigger a distance measurement.

The STM32 sends a 10 microsecond trigger pulse to the ultrasonic sensor, measures the echo pulse duration and calculates the distance. The result is displayed through LEDs and can also be sent through UART.

### Automatic Mode

In automatic mode, the servomotor performs a sweep across several angular positions:

```text
-90°, -45°, 0°, 45°, 90°
```

At each position, the ultrasonic sensor measures the distance. This allows the system to scan its surroundings and detect obstacles in different directions.

## Peripherals Used

### GPIO

GPIO pins are used for LEDs, buttons, trigger signal generation and mode indication.

### TIM2

TIM2 is used to generate the PWM signal required to control the SG90 servomotor.

### TIM3

TIM3 is used for ultrasonic sensor timing.

* Channel 3: generation of the trigger pulse timing
* Channel 4: input capture for echo pulse measurement

### TIM4

TIM4 is used for the rest of time measurments needed

* Channel 1: control timing related to the measurement LED.
* Channel 2: changes in the positions during the automatic sweep

### ADC1

ADC1 is used to read an analog input signal.

### EXTI

External interrupts are used to detect button presses.

* PC13: mode selection button
* PB4: manual measurement button

### USART2

USART2 is used for serial communication and debugging through `printf`.

## Distance Calculation

The HC-SR04 echo pulse duration is measured in microseconds. The distance in centimeters is calculated using:

```c
distance_cm = echo_time_us / 58;
```

This approximation is based on the speed of sound and the round-trip time of the ultrasonic pulse.

## How It Works

1. The STM32 configures GPIOs, timers, ADC, UART and external interrupts.
2. The user selects manual or automatic mode.
3. A 10 microsecond trigger pulse is sent to the HC-SR04 sensor.
4. The echo pulse duration is captured using TIM3.
5. The distance is calculated from the echo time.
6. LEDs and UART output show the measured distance.
7. In automatic mode, the SG90 servo rotates through several angles and repeats the measurement process.

## Skills Demonstrated

* Embedded C programming
* STM32 register-level peripheral configuration
* Timer configuration
* PWM generation
* Input capture
* External interrupts
* ADC reading
* UART communication
* Sensor integration
* Servo motor control
* Embedded system design

## Author

Rodrigo Parente Carrasco  
Telecommunication Engineering Student  
Universidad Carlos III de Madrid  

