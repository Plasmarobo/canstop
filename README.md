# canstop
An open hardware CAN motor controller/endstop with NEMA17 mounting

## Klipper Menuconfig
Select STM32F103
CAN Communication on PA12/PA11
Bootloader: optional, if using katapult select 8k

## Katapult Menuconfig
Select STM32F103
CAN Communication on PA12/PA11

## Memory addresses
Use JTAG to flash firmware
Klipper only: @ address 0x8000000
Katapult + Klipper: Katapult @ 0x8000000, Klipper @ 0x8002000

## Klipper Example config
```
[mcu CANStop0]
canbus_uuid: xxxxxxxx

[output_pin CANStop0_led]
pin: CANStop0: PA0

[led CANStop0_led]
green_pin: CANStop0: PA0
cycle_time: 1
hardware_pwm: True

[stepper_a]
step_pin: CANStop0: PB8
enable_pin: CANStop0: PA8
dir_pin: CANStop0: PB7
endstop_pin: CANStop0: PB12

[temperature_sensor]
sensor_type: mcu
sensor_temperature1:
sensor_adc1:
```

# Hardware Description
At the core is an STM32F103C8T6.
The maximum input voltage is 24V, regulated by an HT7533 down to 3.3V for the STM and other devices.
A 120Ohm terminal resistor is on board, with a Normally Open Solder Jumper.
Footprint is desinged for 90 degree angle XT30 2+2 connectors.
## Pin mapping
* BOOT0: Boot 0 debug port
* PA12: CAN_TX
* PA11: CAN_RX
* PA9: UART/PDN for TMC2209
* PA8: TMC2209 Enable pin
* PB8: TMC2209 Step pin
* PB7: TMC2209 DIR pin

* PB15: CAN Standby Pin
* PB13: EIO Pin
* PB12: ESTOP Pin
* PA2: USER UART TX (debug)
* PA3: USER UART RX (debug)
* PA0: LED1 (active low)
