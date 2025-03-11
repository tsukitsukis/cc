# Neural Orbit
- Name:Ziyi Wang;Keyi Zhang;Qiang Hei
- date:2025.2.12.
## Instructions
- This project integrates p5.js with ESP32 and connects them via OSC, creating an interaction between the virtual and the physical. The ESP32 is embedded within a 3D-printed silver-white sphere, capturing motion data to synchronise the movement of a dynamic virtual sphere in p5.js.
## Feature Overview
### 1. ESP32 + MPU6050 for Motion Data Acquisition
The MPU6050 sensor detects both acceleration and gyroscope data.
The ESP32 connects to the network over Wi-Fi and sends this data to the Node.js server in OSC (Open Sound Control) message format.
### 2. Node.js as an OSC Relay
Using node-osc (or a similar library) and Socket.io, the server receives OSC data from the ESP32.
After parsing the data, it forwards it via Socket.io to the p5.js front-end.
### 3. p5.js for Dynamic Virtual Sphere Rendering
Upon receiving sensor data, the p5.js front-end updates the 3D sphere’s rotation and motion in real time.
The sphere rendered in the browser remains synchronized with the physical sphere’s movements.
## Dependencies & Installation
This project consists of Node.js server, p5.js front-end, and Arduino (ESP32) parts. Please ensure all dependencies are satisfied in each part.
### 1.Node.js Side
Node.js: version 14+ recommended (Download)
NPM: included with Node.js (you may use Yarn or other package managers if preferred)

Main dependencies:express/socket.io/osc

In the project root directory, run the following command to install dependencies:
npm install

If there is no package.json present, you should manually install the required packages, for example:
npm install express socket.io osc open
### 2. p5.js Front-End
p5.js: Front-end drawing library
### 3. Arduino (ESP32) Side
1.Arduino IDE:
version 1.8.19 or higher recommended (Download)

2.ESP32 Board Support：
In Arduino IDE, go to File -> Preferences and add the following link in Additional Boards Manager URLs:
https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json

Then go to Tools -> Board -> Boards Manager, search for esp32, and install it.

3.Required Libraries (use Arduino Library Manager or install via .zip):
WiFi (included with ESP32)
ArduinoOSC: for sending/receiving OSC messages
Adafruit MPU6050: for the MPU6050 sensor
Adafruit Unified Sensor (dependency for Adafruit MPU6050)
## Installation & Usage
### 1.Clone or Download the Project

git clone <Project URL>
cd <Project Folder>

### 2.Install Node.js Dependencies

npm install
### 3.Run the Node.js Server

node app.js

· By default, the server listens on port 3001. Open http://localhost:3001 in your browser to view.

· If the code uses open, the server will automatically open the page in your browser once it starts running.
### 4.Configure and Upload Arduino (ESP32) Code

Open the arduino.ino (or related .ino file) in the Arduino IDE.
Update the Wi-Fi SSID, password, and the target IP address (oscAddress) to match the IP of the computer running the Node.js server.
Connect the ESP32 board via USB, select the correct board and port, and upload the sketch.
Once powered, the ESP32 sends MPU6050 data via OSC to the Node.js server.
### 5.View Real-Time Output

In your browser, go to [Your IP or localhost]:3001 (assuming the computer and ESP32 are on the same local network).
As you move the physical sphere (ESP32 with MPU6050), the p5.js-rendered sphere in the browser will rotate/move accordingly.
