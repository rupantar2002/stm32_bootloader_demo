# STM32 Bootloader with Dual Applications

This project demonstrates the implementation of a custom bootloader for an STM32 microcontroller. The bootloader decides which application (Application1 or Application2) to run based on the state of a GPIO pin (PA0). This workspace includes:

- **Bootloader**: Occupying the first 16 KB of flash.
- **Application1**: Occupying 32 KB of flash, starting at `0x08008000`.
- **Application2**: Occupying 32 KB of flash, starting at `0x08010000`.

---

## Project Structure
```
workspace/
├── Bootloader/
│   ├── Core/
│   │   ├── Src/
│   │   └── Inc/
│   └── ...
├── Application1/
│   ├── Core/
│   │   ├── Src/
│   │   └── Inc/
│   └── ...
├── Application2/
│   ├── Core/
│   │   ├── Src/
│   │   └── Inc/
│   └── ...
└── README.md
```

---

## Bootloader Behavior
1. **Initialization**: The bootloader initializes system peripherals.
2. **GPIO Pin Check**: Reads the state of GPIO pin PA0:
   - **PA0 = 0**: Jumps to Application1 at `0x08004000`.
   - **PA0 = 1**: Jumps to Application2 at `0x08008000`.
3. **Jump to Application**:
   - Sets the stack pointer and jumps to the application start address.

---

## Applications (Application1 and Application2)
Both applications demonstrate the following functionality:

1. **LED Blinking**:
   - Application1 toggles an LED connected to GPIO pin PD15.
   - Application2 toggles an LED connected to GPIO pin PD12.
2. **Debug Output**:
   - Application1 prints `"Application 1 Running...."`.
   - Application2 prints `"Application 2 Running...."`.

---

## Flash Memory Layout
| Component       | Start Address | End Address  | Size    |
|-----------------|---------------|--------------|---------|
| Bootloader      | 0x08000000    | 0x08003FFF   | 16 KB   |
| Application1    | 0x08008000    | 0x0800FFFF   | 32 KB   |
| Application2    | 0x08010000    | 0x08017FFF   | 32 KB   |

---

## Build and Flash Instructions
1. **Bootloader**:
   - Set the flash start address to `0x08000000` in the linker script.
   - Build and flash the bootloader using STM32CubeIDE or another tool.
2. **Application1**:
   - Set the flash start address to `0x08008000` in the linker script.
   - Build and flash Application1.
3. **Application2**:
   - Set the flash start address to `0x08010000` in the linker script.
   - Build and flash Application2.

---

## Testing
1. **Setup**:
   - Connect an LED to GPIO pin PB0 for Application1 and PB1 for Application2.
   - Connect a button to GPIO pin PA0.
2. **Testing Procedure**:
   - Set PA0 to LOW and reset the board:
     - The bootloader will jump to Application1.
     - Observe the LED on PD15 blinking and the debug message `"Application 1 Running...."`.
   - Set PA0 to HIGH and reset the board:
     - The bootloader will jump to Application2.
     - Observe the LED on PD12 blinking and the debug message `"Application 2 Running....g"`.

---

## Areas for Images
1. **Project Diagram**:
   - A diagram illustrating the flash memory layout and the role of the bootloader.
   - Include an image file showing the GPIO pin connections for LEDs and buttons.
2. **Flowchart**:
   - A flowchart describing the bootloader decision-making process.

> **Placeholder**: Add images to the `images/` directory and link them below.

![Project Diagram](images/project_diagram.png)
![Bootloader Flowchart](images/bootloader_flowchart.png)

---

## Enhancements
1. **Checksum Validation**: Add checksum verification before jumping to the application.
2. **Firmware Update**: Implement an update mechanism for OTA or serial updates.
3. **Error Handling**: Add fallback logic in case of application corruption.
3. **Custom Protocol**: Add custom communication protocol logic (`i.e USB or UART`).


---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.
