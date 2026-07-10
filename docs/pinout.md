# Pinout

| Function | Pin | Description |
|---|---|---|
| Ultrasonic Trigger | PC8 | Output signal to start the HC-SR04 measurement |
| Ultrasonic Echo | PC9 | Echo input captured using TIM3 channel 4 |
| Distance LED 1 | PC0 | Distance indicator |
| Distance LED 2 | PC1 | Distance indicator |
| Distance LED 3 | PC2 | Distance indicator |
| Distance LED 4 | PC3 | Distance indicator |
| Distance LED 5 | PC4 | Distance indicator |
| Measurement LED | PB5 | Indicates that a measurement is in progress |
| Manual Measure Button | PB4 | Starts a distance measurement |
| Mode Button | PC13 | Switches between manual and automatic mode |
| Mode LED | PA5 | Indicates automatic mode |
| ADC Input | PA1 | Analog input used to control the servo in manual mode |
| Servo PWM | PA0 / TIM2_CH1 | PWM signal for the SG90 servomotor |
| UART | USART2 | Serial output for debugging and distance information |
