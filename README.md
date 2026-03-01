# Health Assistant Robot 
* An intelligent health assistant robot that provides real-time personalized guidance based on user inputs such as daily routine, food intake, and physical activity.
* It monitors key health metrics like pulse rate and body temperature, and suggests actions such as walking or resting to help maintain a healthy lifestyle.
* The system promotes better habits through interactive feedback, making healthcare guidance simple and accessible.

# Problem
* People lack real-time personalized guidance for daily habits like eating and physical activity.
* This leads to unhealthy lifestyles and increases the risk of diseases such as Type 2 diabetes, obesity, heart disease, and high blood pressure.

# Solution
* Introduces a health assistant robot that analyzes user inputs such as food intake and daily activity.
* Provides real-time personalized suggestions like walking, resting, or maintaining activity levels.
* Helps users adopt a healthier lifestyle through continuous guidance and feedback.
  
# Basic Working 
1️⃣ Voice Interaction
* User speaks through microphone
* MCU sends voice to cloud → converts to text
* Understands what user asked (food, health, etc.)

2️⃣ Sensor Monitoring
* Pulse sensor measures heart rate.
* Temperature sensor measures body temperature.
* MCU collects real-time health data.

3️⃣ Input Processing

* MCU sends user query + sensor data to AI (via WiFi).
* AI analyzes food, health condition, and routine.
* Generates smart suggestions (trainer-level advice).

4️⃣ Output Response

* Robot speaks answer through speaker .
* Shows advice + health score on OLED.
* Gives suggestions like walking, hydration, routine tips.

# Components used 
* ESP32 DevKit,Arduino,Pulse Sensor (heart rate), DS18B20 Temperature Sensor, INMP441 I2S Microphone, PAM8403 Amplifier Module, 8Ω Mini Speaker, 0.96” OLED Display.
* 18650 Lithium Battery, TP4056 Charging Module, MT3608 Boost Converter, 18650 Battery Holder,  toggle/sliding  Switch
* Zero PCB, project box ,Some resistors, capacitors and jumper wires

# Codes/Images and Demo vidoes for testing components on breadboard .
 1. Testing of RGB (for assitant) when switch is on:
    ![Testing of rgb when switch on](https://github.com/user-attachments/assets/d3f27adc-7c9f-4f09-981b-e3c42e50f044)
 2. Testing of RGB(for assistant) when switch is off:
    ![Testing of rgb when switch off ](https://github.com/user-attachments/assets/1d893a60-3b34-423b-8132-33b84155a41f)
    
 # Code
// Pin Definitions
const int SWITCH_PIN = 4;
const int GREEN_LED  = 6;
const int RED_LED    = 5;
// Blink timing
const int BLINK_DELAY = 300;
void setup() {
  pinMode(SWITCH_PIN, INPUT_PULLUP);
  pinMode(GREEN_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
}
void loop() {
  // Read switch state (LOW = pressed)
  bool isPressed = (digitalRead(SWITCH_PIN) == LOW);

  if (isPressed) {
    handlePressedState();
  } else {
    handleReleasedState();
  }
}
//  When button is pressed
void handlePressedState() {
  digitalWrite(GREEN_LED, HIGH);  // Green ON
  digitalWrite(RED_LED, LOW);     // Red OFF
}
//  When button is released
void handleReleasedState() {
  digitalWrite(GREEN_LED, LOW);   // Green OFF

  // Red blinking
  digitalWrite(RED_LED, HIGH);
  delay(BLINK_DELAY);

  digitalWrite(RED_LED, LOW);
  delay(BLINK_DELAY);
}

 4. Testing Video of buzzer with toggle switch :
    https://github.com/user-attachments/assets/0686ec95-1307-42ac-9540-21d9e520734c
    
 # Code
// Pin Configuration
// =====================
const int SWITCH_PIN = 4;
const int GREEN_LED  = 6;
const int RED_LED    = 5;
const int BUZZER_1   = 7;
const int BUZZER_2   = 8;

// =====================
// Setup Function
// =====================
void setup() {
  pinMode(SWITCH_PIN, INPUT);
  pinMode(GREEN_LED, OUTPUT);
  pinMode(RED_LED, OUTPUT);
  pinMode(BUZZER_1, OUTPUT);
  pinMode(BUZZER_2, OUTPUT);
}

// =====================
// Main Loop
// =====================
void loop() {
  bool isSwitchOn = digitalRead(SWITCH_PIN);

  if (isSwitchOn) {
    handleSystemActive();
  } else {
    handleSystemInactive();
  }
}

// =====================
// Active State (Switch ON)
// =====================
void handleSystemActive() {
  digitalWrite(GREEN_LED, HIGH);  // Green ON
  digitalWrite(RED_LED, LOW);     // Red OFF

  playGreetingTone();             // Play "Good Afternoon" tone
}

// =====================
// Inactive State (Switch OFF)
// =====================
void handleSystemInactive() {
  digitalWrite(GREEN_LED, LOW);   // Green OFF
  digitalWrite(RED_LED, HIGH);    // Red ON

  stopBuzzer();                   // Ensure buzzer is OFF
}

// =====================
// Greeting Tone Function
// =====================
void playGreetingTone() {
  // "Good"
  tone(BUZZER_1, 400); tone(BUZZER_2, 500); delay(120);
  tone(BUZZER_1, 500); tone(BUZZER_2, 600); delay(120);

  // Pause
  stopBuzzer(); delay(80);

  // "After"
  tone(BUZZER_1, 450); tone(BUZZER_2, 550); delay(150);
  tone(BUZZER_1, 500); tone(BUZZER_2, 650); delay(150);

  // Pause
  stopBuzzer(); delay(100);

  // "Noon"
  tone(BUZZER_1, 600); tone(BUZZER_2, 700); delay(200);
  tone(BUZZER_1, 500); tone(BUZZER_2, 600); delay(300);

  stopBuzzer();
}

// =====================
// Stop Buzzer Function
// =====================
void stopBuzzer() {
  noTone(BUZZER_1);
  noTone(BUZZER_2);
}
     
 5. Some(20-30%) components of assitant:
    ![some components 1](https://github.com/user-attachments/assets/6ebd865e-6bb1-4ab7-a2a6-20af320a3523)
    ![Some Components ](https://github.com/user-attachments/assets/50e4a05d-94ba-4507-a69e-b3434ccd1f1e)

#  Current Progress(20-30%)
The initial prototype has been successfully tested with the following components:
* RGB LED for status indication
* Buzzer for alert system in assitant
* Power supply using rechargeable battery
* TP4056 charging module for battery management
* Buck converter for voltage regulation

#  Hardware Setup
The system is powered using a rechargeable battery connected through a TP4056 charging module. A buck converter is used to regulate the voltage and ensure stable power supply to the MCU and other components.

# Remaining implementation will be done during hackathon like:
* Integration of  pulse, temperature sensors and other hardware components.
* Implementation of  decision-making logic for health suggestions
* Display real-time feedback on LCD/OLED and emotion for the assitant 
* Adding interaction using buttons or voice input
* Setting up with API and cloud( software part).

# Future Scope
1. Mobile App and Cloud Tracking
  * Store daily health data
  * Show graphs & reports
    
2. Elderly Care & Emergency Support
  * Detect abnormal pulse/temp.
  * Send alert to family.
Can be used for home & healthcare.

