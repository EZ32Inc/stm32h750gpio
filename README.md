# STM32H750 GPIO LED Toggle Demo for use with ESP32JTAG and VSCode+Cortex-debug 

This project demonstrates a minimal STM32H750 GPIO LED toggle example built using:

- arm-none-eabi-gcc
- Makefile
- STM32CubeMX (code generation only)
- ESP32JTAG and VSCode+Cortex-debug for debugging 

---

# How to use this project

## Step 1 — Install ARM GCC Toolchain (Linux / Ubuntu) if you have not

```bash
sudo apt update
sudo apt install gcc-arm-none-eabi make
```

Verify installation:

```bash
arm-none-eabi-gcc --version
```

## Step 2 — Install VScode then install Cortex-debug

Google or ask AI, it is easy and free!


## Step 3 — flash and debug the MCU 

### Using ESP32JTAG with VSCode+Cortex-debug

Install VSCode and then the Cortex-debug extention:

Then run VSCode and open this folder.
We already have inlcuded a setup file in .vscode/lauch.json, you may need to change the IP address of ESP32JTAG if it is not 192.168.4.1
```
{
  "version": "0.2.0",
  "configurations": [

    {
      "name": "ESP32JTAG Debug",
      "cwd": "${workspaceFolder}",
      "executable": "build/stm32h750gpio.elf",
      "request": "launch",
      "type": "cortex-debug",
      "servertype": "external",
      //"gdbTarget": "192.168.2.42:4242",
      "gdbTarget": "192.168.4.1:4242",
      "device": "STM32F750",
      //"showDevDebugOutput": "raw",
      "interface": "swd",
      "runToEntryPoint": "main",
      "preLaunchTask": "build",
      //"preLaunchCommands": [
       "overrideLaunchCommands":[
        "file build/stm32h750gpio.elf",
        "enable breakpoint",
        "monitor a",
        "attach 1",
        "load"
      ]

    }
  ]
}
```
Then press F5 to start to flash and debugging!

---

# How to create a project like this (Step 1 → Step 5)

## Step 1 — Install STM32CubeMX

Download STM32CubeMX from STMicroelectronics official website and install it.

STM32CubeMX is only used to generate project skeleton code.  
No IDE is required for development.

---

## Step 2 — Create STM32H750 Project

###You can create a project for other STM MCUs the same way.

1. Open STM32CubeMX
2. Click **New Project**
3. Select your exact STM32H750 part number
4. Go to **Pinout & Configuration**
5. Configure one GPIO pin as:

   - Mode: Output Push-Pull  
   - Example: `PA5` (if LED is connected there)

---

## Step 3 — Configure Project Toolchain

In STM32CubeMX:

1. Go to **Project Manager**
2. Set **Toolchain / IDE** to:

```
Makefile
```

3. Generate Code

You will now have a project structure similar to:

```
Core/
Drivers/
startup_stm32h750xx.s
STM32H750xx_FLASH.ld
Makefile
```

---

## Step 4 — Add LED Toggle Code

Open:

```
Core/Src/main.c
```

Inside the main loop:

```c
while (1)
{
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(500);
}
```

Adjust GPIO port and pin according to your hardware.

---

## Step 5 — Build the Project

From project root directory:

```bash
make
```

Build outputs will be generated in:

```
build/project.elf
build/project.bin
build/project.hex
```

To clean:

```bash
make clean
```

---


# What This Demo Does

- Initializes system clock
- Configures one GPIO as output
- Toggles LED every 500ms
- Demonstrates GCC + Makefile workflow
- Using ESP32JTAG with VSCode+Cortex-debug to flash and debug STM32H750 target

---

# Recommended Extensions

- Replace HAL delay with SysTick-based delay
- Add UART printf
- Add button interrupt
- Add FreeRTOS
- Convert to bare-metal (no HAL)

---

Author: Andrew Li  
License: MIT
