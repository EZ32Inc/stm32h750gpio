# stm32h750gpio
flowchart TD

    A[Start: STM32H750 GPIO LED Demo Setup] --> B[Step 1: Install ARM GCC Toolchain]

    B --> B1[Run:
    sudo apt install gcc-arm-none-eabi make]

    B1 --> B2[Verify:
    arm-none-eabi-gcc --version]

    B2 --> C[Step 2: Install STM32CubeMX]

    C --> C1[Download from STMicroelectronics website]
    C1 --> C2[Install and launch STM32CubeMX]

    C2 --> D[Step 3: Create STM32H750 Project]

    D --> D1[New Project]
    D1 --> D2[Select STM32H750 MCU (exact package)]
    D2 --> D3[Pinout & Configuration]
    D3 --> D4[Enable one GPIO as Output Push-Pull (e.g., PA5)]

    D4 --> E[Step 4: Configure Project Settings]

    E --> E1[Project Manager → Toolchain: Makefile]
    E1 --> E2[Generate Code]

    E2 --> E3[Generated Structure:
    Core/
    Drivers/
    Makefile
    startup_stm32h750xx.s
    linker_script.ld]

    E3 --> F[Step 5: Add LED Toggle Code]

    F --> F1[Open: Core/Src/main.c]
    F1 --> F2[Inside while(1):
    
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
    HAL_Delay(500);]

    F2 --> G[Step 6: Build Project]

    G --> G1[Run:
    make]

    G --> G2[Output:
    build/project.elf
    build/project.bin]

    G2 --> H[Done]

