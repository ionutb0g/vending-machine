# Final Robotics Project - Mini Vending Machine

-----------------------------------------------------------------------------------------------------

## 🚀 Project Overview

This project implements a **miniaturized robotic vending machine** capable of dispensing products upon user interaction. The machine supports item selection via a 4×4 button matrix and RFID card authentication. The core controller is an **ESP32**, which handles hardware control, local logic, and **Wi-Fi connectivity** for a companion web application (for stock management, user accounts, and online card validation).

A fully offline MVP will dispense items based solely on local input and a dummy RFID card to validate basic mechanics and electronics.

-----------------------------------------------------------------------------------------------------

## 📦 Bill of Materials (BOM)

| Component                 | Quantity | Notes                               |
|---------------------------|----------|-------------------------------------|
| ESP32 Development Board   | 1        | Central controller with Wi-Fi       |
| NEMA 17 Stepper Motor     | 4        | One per product channel             |
| Servo Motor               | 1        | Controls the front door latch       |
| RFID Scanner              | 1        | For demo credit card authentication |
| 4×4 Button Matrix         | 1        | User item selection                 |
| 16×2 LCD Display          | 1        | User feedback and status            |
| Stepper Motor Drivers     | 4        | e.g. A4988 or DRV8825               |
| Misc Electronics          | —        | Wires, headers, resistors, cables   |
| 3D Printed Frame          | —        | Custom structural enclosure         |

-----------------------------------------------------------------------------------------------------

## 📚 Tutorial Source (Inspiration)

This project’s mechanical and control logic inspiration is informed by DIY vending machine examples that use microcontrollers, LCDs, buttons, and motor drives.

[Main inspiration for this project](https://vm.tiktok.com/ZNRhy9WXq/)

I am aiming to replicate the core vending functionalities demonstrated in the inspiration project while bringing my own modifications, especially the addition of a Wi-Fi–enabled web application for real-time stock monitoring, remote configuration, and online RFID card validation.

-----------------------------------------------------------------------------------------------------

### **What is the system boundary?**

The system includes all hardware and software required to *dispense products*, *accept user input*, *authenticate an RFID card*, and *report status*.  
Inputs: button matrix, RFID card.  
Outputs: stepper actions, servo latch, LCD status, and web app telemetry.

All item selection and dispense logic run locally on the ESP32; optional cloud interactions are part of the extended webapp layer.

### **Where does intelligence live?**

Intelligence resides in the **ESP32 microcontroller**:

- It reads user input and RFID scans.
- Decides what item to vend.
- Controls motor actions and latch servo.
- Interfaces with Wi-Fi for web app interaction.

Higher-level business rules and stock persistence are optionally handled by the **web application**.

### **What is the hardest technical problem?**

The hardest technical challenge is designing the system to be scalable and expandable. Each additional product requires an additional stepper motor and driver, which in turn requires more GPIO pins for control. A naive design quickly runs out of pins on the ESP32.

The core difficulty is therefore architectural:

how to support more motors than available pins

how to avoid redesigning the entire circuit when expanding

how to keep wiring and firmware manageable as the system grows

This involves evaluating options such as I/O expanders, motor driver buses, shift registers, multiplexers, or communication-based motor control modules. The solution must balance cost, electrical complexity, and software complexity while ensuring future vending slots can be added without redesigning the whole controller.

### **What is the minimum demo?**

An offline MVP that:

- Accepts a selection via the button matrix.
- Reads a dummy RFID card and confirms valid.
- Moves the correct stepper motor to dispense an item.
- Displays status on the LCD.

No Wi-Fi or backend connectivity is required for the minimum demo.

### **Why is this not just a tutorial?**

Though inspired by tutorials, this project expands functionality significantly by:

- Integrating a **web service backend**.
- Enabling **real-time stock monitoring** and remote operations.
- Designing a custom **3D-printed frame**.
- Using an ESP32 (Wi-Fi capable) rather than basic Arduino platforms.
- Solving non-trivial integration challenges between embedded hardware and web infrastructure.

This moves it beyond a simple how-to rebuild.

## ❓ Do You Need an ESP32?

YES. The ESP32 is required for:

- Handling GPIO for motors, buttons, RFID.
- Running local logic and a web server.
- Connecting to the local network for stock and validation UI.

Without Wi-Fi connectivity, you would lose the **web-app extension** and dynamic stock/validation features.