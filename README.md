# Traffic-light-Control-using-blynk-and-Nodemcu-esp32



This IoT project uses the Blynk platform and ESP32 (NodeMCU-ESP8266 module) to simulate and control a traffic light system. Users can remotely monitor and operate the system via a mobile app or browser interface using Blynk.

Table of Contents

Project Overview

Tech Stack

System Components

Features

Circuit Diagram

Code Explanation

Simulation

Output

Getting Started

License


Project Overview

The main goal of this project is to control traffic lights remotely using IoT tools. It utilizes Blynk for remote control and ESP32 for hardware control. The system simulates a real-world traffic light setup with three LEDs, each operated via a virtual switch in the Blynk app.


Tech Stack

Hardware: ESP32 / NodeMCU-ESP8266

Software: Blynk Console, Arduino IDE

Simulation Tool: Wokwi

Language: C++ (Arduino)


System Components

ESP32 – WiFi-enabled microcontroller

Blynk – IoT platform for controlling hardware

LEDs – Represent traffic signals

Wokwi – For simulation and debugging

Features

Remote traffic light control via Blynk mobile/web app

Real-time status update of each signal

OTA (Over-the-Air) updates support

Low-power and scalable IoT design


Code Explanation

#define BLYNK_TEMPLATE_ID "TMPL3-B6Qx-Qf"
#define BLYNK_TEMPLATE_NAME "TLIGHTS"
#define BLYNK_AUTH_TOKEN "your_auth_token"

#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

const char* ssid = "Wokwi-GUEST";
const char* password = "";

#define RELAY1_PIN  25
#define RELAY2_PIN  26
#define RELAY3_PIN  27

#define SWITCH1_VPIN V0
#define SWITCH2_VPIN V1
#define SWITCH3_VPIN V2

// Virtual pin handlers for Blynk buttons
BLYNK_WRITE(SWITCH1_VPIN) {
  digitalWrite(RELAY1_PIN, param.asInt() ? HIGH : LOW);
}
BLYNK_WRITE(SWITCH2_VPIN) {
  digitalWrite(RELAY2_PIN, param.asInt() ? HIGH : LOW);
}
BLYNK_WRITE(SWITCH3_VPIN) {
  digitalWrite(RELAY3_PIN, param.asInt() ? HIGH : LOW);
}

void setup() {
  Serial.begin(115200);
  for (int pin : {RELAY1_PIN, RELAY2_PIN, RELAY3_PIN}) {
    pinMode(pin, OUTPUT);
    digitalWrite(pin, LOW);
  }

  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("\nWiFi connected");

  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, password);
}

void loop() {
  Blynk.run();
}

> Note: Replace "your_auth_token" with your actual token from Blynk.

Simulation

The system was simulated using Wokwi, which provides:

WiFi simulation

Logic analyzers

Debugging via GDB

Visual Studio Code integration

Output

Control traffic lights (Red, Yellow, Green LEDs) directly from your smartphone using the Blynk app. LED states are updated instantly based on your inputs.

Getting Started

1. Install Blynk IoT app on your phone
2. Create a new template with the given ID, Name, and Auth token
3. Upload the code to ESP32 using Arduino IDE
4. Connect to "Wokwi-GUEST" or your preferred network
5. Simulate or run on hardware to test



License

This project is open-source and available under the MIT License.



