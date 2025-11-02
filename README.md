# AutomaticNightLight

##  Overview
This project demonstrates how to use a **Light Dependent Resistor (LDR)** with an **Arduino Uno** to detect light levels.  
When it gets dark, an **LED automatically turns ON**, and when it’s bright, the LED turns OFF.  

---

## Components Required

| Component | Quantity | Description |
|------------|-----------|-------------|
| Arduino Uno | 1 | Main microcontroller board |
| LDR (Light Dependent Resistor) | 1 | Light sensor |
| LED | 1 | Output light |
| 220Ω Resistor | 1 | Limits current through LED |
| Jumper Wires | Several | For making connections |

---

##  Circuit Connections

###  LED:
- **Anode (long leg)** → **Digital Pin 9** (through a **220Ω resistor**)  
- **Cathode (short leg)** → **GND**

###  LDR:
- One leg → **5V**  
- Other leg → **A0**  
- Also connect **A0** → **GND** with a **jumper wire**  
  *(This simple setup acts as a basic voltage divider. For more accuracy, you can later add a 10kΩ resistor between A0 and GND.)*

---

##  Arduino Code

```cpp
// AutomaticNightLight LDR and Arduino Uno
// LED turns ON when it's dark

int ldrPin = A0;    // LDR connected to analog pin A0
int ledPin = 9;     // LED connected to pin 9
int ldrValue = 0;   // To store LDR reading
int threshold = 500; // Adjust based on your lighting conditions

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600); // For monitoring LDR readings
}

void loop() {
  ldrValue = analogRead(ldrPin);  // Read light sensor value
  Serial.println(ldrValue);       // Print reading to Serial Monitor

  if (ldrValue < threshold) {
    digitalWrite(ledPin, HIGH);   // It's dark — turn LED ON
  } else {
    digitalWrite(ledPin, LOW);    // It's bright — turn LED OFF
  }

  delay(200); // Small delay for stability
}
