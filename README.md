# Smart-Door-Lock

This project demonstrates how to create a smart RFID-based door lock system using an ESP8266 microcontroller, MFRC522 RFID reader, and Blynk for remote control and monitoring. Authorized access is granted via specific RFID tags, and the system can be controlled via the Blynk app.

## Table of Contents

- [Components Required](#components-required)
- [Circuit Connections](#circuit-connections)
- [Software Requirements](#software-requirements)
- [Setup Instructions](#setup-instructions)
  - [1. Configure Blynk](#1-configure-blynk)
  - [2. Code Configuration](#2-code-configuration)
  - [3. Upload the Code](#3-upload-the-code)
  - [4. Wiring](#4-wiring)
  - [5. Running the System](#5-running-the-system)
  - [6. Blynk App Features](#6-blynk-app-features)
- [RFID UIDs Configuration](#rfid-uids-configuration)
- [Future Improvements](#future-improvements)
- [License](#license)

## Components Required

- ESP8266 (e.g., NodeMCU or Wemos D1 Mini)
- MFRC522 RFID reader module
- Servo motor (for the door lock mechanism)
- LEDs (Green and Red for status indication)
- Buzzer (for access feedback)
- Jumper wires
- Power supply (e.g., USB)
- Blynk app installed on your smartphone

## Circuit Connections

| Component   | ESP8266 Pin |
|-------------|-------------|
| MFRC522 SS  | D4          |
| MFRC522 RST | D3          |
| Green LED   | D1          |
| Red LED     | D2          |
| Buzzer      | D8          |
| Servo       | D0          |

## Software Requirements

1. **Arduino IDE**: For writing and uploading code to the ESP8266.
2. **Blynk App**: Available on both Android and iOS platforms.

### Libraries to Install

Install the following libraries in Arduino IDE:
- `MFRC522` (for the RFID module)
- `Servo` (for controlling the servo motor)
- `BlynkSimpleEsp8266` (for communication with Blynk Cloud)

## Setup Instructions

### 1. Configure Blynk

- Install the Blynk app on your smartphone.
- Create a new project in Blynk and select ESP8266 as the device.
- Add widgets to control and monitor the system:
  - Terminal on Virtual Pin V2
  - Button widgets for Virtual Pin V3, V4, and V5
- Obtain the `BLYNK_TEMPLATE_ID` and `BLYNK_AUTH_TOKEN` from the Blynk app.

### 2. Code Configuration

Before uploading the code to the ESP8266, update the following in the code:

- Replace `BLYNK_TEMPLATE_ID` and `BLYNK_AUTH_TOKEN` with your unique IDs from Blynk.
- Update the Wi-Fi credentials (`ssid` and `pass`) with your network details.
- Update the RFID card UIDs in the code (for authorized access).

```cpp
#define BLYNK_TEMPLATE_ID "xxxxxxxx"   // Enter the template ID
#define BLYNK_AUTH_TOKEN  "xxxxxxxxxx" // Enter the Blynk Auth Token
char ssid[] = "YourNetworkSSID";       // Enter your Wi-Fi SSID
char pass[] = "YourNetworkPassword";   // Enter your Wi-Fi Password
```

### 3. Upload the Code

- Connect your ESP8266 to your PC.
- Select the correct board (e.g., NodeMCU 1.0) and COM port in the Arduino IDE.
- Upload the code.

### 4. Wiring

Connect the RFID reader, servo, LEDs, and buzzer as per the circuit diagram (detailed above) and power on the system.

### 5. Running the System

Once powered, the system will:
- Read RFID cards using the MFRC522 module.
- Grant or deny access based on the card's UID.
- Indicate access status with LEDs and a buzzer.
- Control the servo motor to lock or unlock the door.
- Send status updates to the Blynk app.

### 6. Blynk App Features

- **Terminal (V2)**: Displays the current user and access status.
- **Button (V3, V4, V5)**: Enable or disable access for different users by toggling these buttons.

 ### RFID UIDs Configuration

Replace the UID strings (`01 94 E1 26`, `60 27 5B 21`, etc.) with the UIDs of your RFID cards in the following code sections:

```cpp
if ((content.substring(1) == "01 94 E1 26") && (fflag == 1)) // Example for first authorized user
if ((content.substring(1) == "60 27 5B 21") && (eflag == 1)) // Example for second authorized user
if ((content.substring(1) == "30 15 B5 20") && (jflag == 1)) // Example for third authorized user
```

## Future Improvements

- Add more user RFID tags by extending the code logic.
- Integrate a relay module to control an actual door lock mechanism.
- Enhance security by adding password-based access along with RFID.

## License

This project is open-source and free to use. Feel free to modify and distribute it as needed.
