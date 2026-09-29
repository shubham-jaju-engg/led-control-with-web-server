# 🌐 ESP32 Web Server for LED Control Using a Web Browser

## 📌 Project Overview

* This project implements a **web-based LED control system using an ESP32**.
* The ESP32 is configured as a **Wi-Fi Access Point (SoftAP)**.
* A web server runs directly on the ESP32.
* A user can connect to the ESP32's Wi-Fi network using a smartphone or computer.
* After connecting, the user can open a web browser and access the ESP32's IP address.
* A simple web page is hosted by the ESP32.
* The web page provides controls for turning connected LEDs **ON and OFF**.
* When the user interacts with the webpage, an HTTP request is sent to the ESP32.
* The ESP32 processes the request and changes the corresponding GPIO output.
* This allows LEDs to be controlled wirelessly without requiring a physical switch.

---

## 🧰 Components Required

### Hardware

* ESP32 Development Board
* LEDs
* 220Ω resistors
* Breadboard
* Jumper wires
* USB cable
* Computer or smartphone with Wi-Fi

### Software

* Arduino IDE
* ESP32 Board Package
* Web Browser

---

## 🔌 Hardware Connections

The project uses ESP32 GPIO pins to control the LEDs.

Example:

| Component    | ESP32                      |
| ------------ | -------------------------- |
| LED 1        | GPIO 16                    |
| LED 2        | GPIO 17                    |
| LED cathodes | GND                        |
| LED anodes   | GPIO through 220Ω resistor |

> The GPIO numbers should match the pin definitions used in the Arduino code.

---

## 🌐 System Architecture

```text
             Smartphone / Computer
                     │
                     │ Wi-Fi
                     ↓
             ┌───────────────┐
             │     ESP32     │
             │               │
             │  Wi-Fi AP     │
             │      +        │
             │  Web Server   │
             └───────┬───────┘
                     │
                GPIO Signals
                 /         \
                ↓           ↓
             LED 1        LED 2
```

---

## ⚙️ How the Project Works

### 1. ESP32 creates a Wi-Fi network

* The ESP32 is configured to work in **Access Point (AP) mode**.
* It creates its own Wi-Fi network.
* A smartphone or computer can connect directly to this network.
* An internet connection is **not required** for controlling the LEDs.

---

### 2. ESP32 starts a web server

* After creating the Wi-Fi network, the ESP32 starts a web server.
* The server listens for incoming HTTP requests.
* The project uses **port 80**, which is the standard port for HTTP communication.

```text
Browser
   ↓
HTTP Request
   ↓
ESP32 Web Server
```

---

### 3. User opens the ESP32 webpage

* The user connects their device to the ESP32's Wi-Fi network.
* The ESP32 assigns an IP address to the connected device.
* The user enters the ESP32's IP address into a web browser.
* The browser sends an HTTP request to the ESP32.
* The ESP32 responds by sending an HTML webpage.

---

### 4. Webpage provides LED controls

* The ESP32-generated webpage contains buttons or links for controlling the LEDs.
* For example:

```text
+---------------------------+
|       ESP32 LED Control   |
|                           |
|       LED 1: [ ON ]       |
|       LED 1: [ OFF ]      |
|                           |
|       LED 2: [ ON ]       |
|       LED 2: [ OFF ]      |
+---------------------------+
```

* Clicking a button generates a corresponding HTTP request.

---

### 5. ESP32 processes the HTTP request

For example, when the user clicks an ON button:

```text
User clicks LED ON
        ↓
Browser sends HTTP request
        ↓
ESP32 receives request
        ↓
ESP32 identifies requested action
        ↓
GPIO is set HIGH
        ↓
LED turns ON
```

Similarly, clicking OFF results in:

```text
User clicks LED OFF
        ↓
Browser sends HTTP request
        ↓
ESP32 receives request
        ↓
GPIO is set LOW
        ↓
LED turns OFF
```

---

## 🔄 Complete Data Flow

```text
        User
         │
         ↓
    Web Browser
         │
         │ HTTP Request
         ↓
   Wi-Fi Connection
         │
         ↓
       ESP32
         │
         ↓
    Web Server
         │
         ↓
   Request Parsing
         │
         ↓
    GPIO Control
       /     \
      ↓       ↓
    LED 1   LED 2
```

---

## 🧠 Program Working

* The ESP32's Wi-Fi functionality is initialized using the `WiFi.h` library.
* The ESP32 is configured as a **Soft Access Point** using `WiFi.softAP()`.
* An SSID and password can be configured for the Wi-Fi network.
* A `WiFiServer` object is created to run the web server.
* The server listens on **TCP port 80**.
* GPIO pins connected to the LEDs are configured as outputs.
* The ESP32 continuously checks whether a client has connected to the web server.
* When a browser sends an HTTP request, the ESP32 reads the incoming request.
* The requested URL/path is examined to determine which LED operation was requested.
* The appropriate GPIO pin is set HIGH or LOW.
* The ESP32 sends an HTTP response containing the webpage back to the browser.
* The browser displays the updated webpage.
* This process repeats continuously, allowing the user to control the LEDs in real time.

---

## 📡 Communication Used

The project uses multiple layers of communication:

```text
Application Layer
        ↓
       HTTP
        ↓
Transport Layer
        ↓
       TCP
        ↓
Network Layer
        ↓
       IP
        ↓
Data Link / Physical
        ↓
       Wi-Fi
```

### HTTP

* HTTP stands for **HyperText Transfer Protocol**.
* It is used for communication between the web browser and the ESP32 web server.
* The browser sends an HTTP request.
* The ESP32 sends an HTTP response.

### TCP

* HTTP communication uses TCP.
* TCP provides reliable communication between the browser and ESP32.

### IP Address

* The ESP32 is assigned an IP address when operating as an Access Point.
* The browser uses this IP address to communicate with the ESP32 web server.

### Port 80

* Port 80 is the standard port used for HTTP.
* The ESP32 web server listens for HTTP connections on this port.

---

## 🖥️ ESP32 Web Server Concept

The ESP32 performs two major tasks simultaneously:

```text
             ESP32
               │
       ┌───────┴───────┐
       ↓               ↓
    Wi-Fi           GPIO
       ↓               ↓
 Web Server         LEDs
       ↓
 Web Browser
```

This demonstrates how a microcontroller can combine:

* Wireless communication
* Networking
* Web technologies
* Embedded programming
* GPIO control

---

## 🔄 Example Request Flow

Suppose the user wants to turn ON LED 1.

```text
Browser
   │
   │ HTTP GET Request
   ↓
ESP32 Web Server
   │
   │ Detect LED 1 command
   ↓
GPIO 16 → HIGH
   │
   ↓
LED 1 ON
   │
   ↓
HTTP Response
   │
   ↓
Browser displays webpage
```

---

## 🛠️ Technologies and Concepts Used

* ESP32
* Arduino IDE
* Embedded C/C++
* Wi-Fi
* Wi-Fi Access Point / SoftAP
* Web Server
* HTTP
* TCP/IP
* IP Addressing
* Port 80
* HTML
* GPIO
* Digital Output
* Client-Server Architecture
* Wireless Device Control

---

## 📚 Important Arduino/ESP32 Functions Used

### `WiFi.softAP()`

* Creates a Wi-Fi Access Point using the ESP32.
* Allows nearby devices to connect directly to the ESP32.

### `WiFiServer server(80)`

* Creates a web server that listens on port 80.

### `server.begin()`

* Starts the web server.

### `server.available()`

* Checks whether a client has connected to the server.

### `client.read()`

* Reads data received from the web browser.

### `digitalWrite()`

* Controls the output state of the LED GPIO pins.

### `Serial.begin()`

* Initializes serial communication for debugging and monitoring.

---

## 📁 Project Structure

```text
ESP32-Web-Server-LED-Control/
│
├── ESP32-Web-Server-LED-Control.ino
├── README.md
└── circuit/
    └── circuit-diagram.png
```

---

## 🚀 How to Run the Project

1. Install the **Arduino IDE**.
2. Install the ESP32 board package.
3. Connect the ESP32 to the computer using USB.
4. Open the `.ino` source file.
5. Select the appropriate ESP32 board and COM port.
6. Upload the program to the ESP32.
7. Open the Serial Monitor.
8. The ESP32 creates its own Wi-Fi network.
9. Connect your smartphone/computer to the ESP32 Wi-Fi network.
10. Open a web browser.
11. Enter the ESP32's IP address.
12. The LED control webpage will appear.
13. Use the webpage controls to turn the LEDs ON or OFF.

---

## 🎯 Applications

* Wireless LED control
* Smart-home prototypes
* IoT projects
* Home automation
* Wireless appliance control
* Embedded web servers
* Remote GPIO control
* ESP32 networking experiments

---

## 🚀 Future Improvements

The project can be extended by:

* Adding more GPIO-controlled devices.
* Adding a responsive/mobile-friendly webpage.
* Adding LED status indicators on the webpage.
* Adding password-protected web access.
* Connecting the ESP32 to an existing Wi-Fi router instead of using SoftAP mode.
* Controlling relays instead of LEDs.
* Adding sensors and displaying sensor readings on the webpage.
* Adding WebSocket communication for faster real-time control.
* Creating a dashboard for multiple devices.
* Adding MQTT for IoT-based communication.
* Controlling the ESP32 remotely through an internet-connected architecture.

---
