# LAB-3

This circuit consists of an Arduino Uno connected to a breadboard, featuring an LED and a Light Dependent Resistor (LDR) (photoresistor). The setup appears to be a light-sensitive LED control system, where the LED responds to changes in ambient light.

Components & Connections:
	1.	Arduino Uno:
	•	Provides power and processes input from the LDR.
	•	Controls the LED based on light intensity.
	2.	LED (Red):
	•	Anode (+) is connected to an Arduino digital output pin (likely pin 9 or 10).
	•	Cathode (-) is connected to GND via a current-limiting resistor.
	3.	LDR (Photoresistor):
	•	Connected in a voltage divider circuit with a fixed resistor.
	•	One leg of the LDR is connected to 5V.
	•	The other leg is connected to an analog input pin (likely A0) and to GND via a resistor.
	•	The voltage at the junction between the LDR and resistor is sent to the Arduino to measure light intensity.
	4.	Resistors:
	•	One resistor limits the LED current.
	•	Another resistor (possibly 10kΩ) forms a voltage divider with the LDR.
	5.	Wiring Summary:
	•	LDR & Resistor: Create a voltage divider that provides an analog signal.
	•	Arduino Analog Pin (A0): Reads voltage changes from the LDR circuit.
	•	Arduino Digital Pin (9 or 10): Controls the LED.
	•	GND & 5V: Provide power to the circuit.

Functionality:
	•	The LDR detects ambient light.
	•	When it is bright, resistance is low, and the voltage read by the Arduino is high.
	•	When it is dark, resistance increases, lowering the voltage.
	•	The Arduino processes this voltage and turns the LED ON in darkness and OFF in brightness.

Arduino Code for Light-Activated LED:

const int ledPin = 9;   // LED connected to pin 9
const int ldrPin = A0;  // LDR connected to analog pin A0
int ldrValue = 0;       // Variable to store LDR value

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600); // For monitoring LDR values
}

void loop() {
  ldrValue = analogRead(ldrPin); // Read LDR value
  Serial.println(ldrValue); // Print LDR value for debugging

  if (ldrValue < 500) {  // Adjust threshold based on lighting conditions
    digitalWrite(ledPin, HIGH);  // Turn LED ON in darkness
  } else {
    digitalWrite(ledPin, LOW);   // Turn LED OFF in bright light
  }

  delay(100);  // Small delay for stability
}

How It Works:
	1.	The Arduino reads the LDR sensor value.
	2.	If the reading is below a threshold (indicating darkness), the LED turns ON.
	3.	If the reading is above the threshold (indicating brightness), the LED turns OFF.
	4.	The Serial Monitor can be used to fine-tune the threshold value.

Possible Enhancements:
	•	Adjust brightness using PWM (analogWrite) for gradual fading.
	•	Add an LCD display to show light intensity values.
	•	Store calibration data for different lighting conditions.

