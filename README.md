# 🤖 RoBOBOt

**RoBOBOt** is a small interactive robot, designed as a friendly companion for children or individuals who may feel lonely. This mini robotic pet combines sound, light, movement, and facial expressions to simulate emotional responses and encourage human interaction.

## 💡 Project Overview

RoBOBOt reacts to different types of touch using a capacitive sensor:
- A **gentle touch** triggers calm sounds and smooth movements.
- A **more energetic touch** triggers playful behavior and lively sound effects.

By combining visual expressions (via an OLED display), motion (using two servo motors), and sound (through buzzers), RoBOBOt aims to offer emotional support, especially to children learning to express and recognize feelings, or to adults seeking a soothing presence.


## 🧰 Hardware Components

- 🔌 ESP32-WROOM-32S Development Board
- ⚙️ SG90 Servo Motors ×2
- 🔊 Passive Buzzers ×2
- 🔴 Red LED ×1
- 👆 TTP223 Capacitive Touch Button ×1
- 📺 0.96” OLED Display
- 🧠 Robot body (custom housing)
- 🔌 USB Data Cable

## 🧱 Assembly Highlights

The robot is split into two main sections:
1. **Base Unit** — Contains the ESP32 board, buzzers, and a capacitor for electrical noise filtering.
2. **Upper Body** — Includes the OLED display, touch sensor, LED, and servo motors to animate arms and body rotation.

## 🧠 Functional States

RoBOBOt operates through **three main behavioral states**:
- 💤 `SLEEPING`: Idle state with minimal activity.
- 😀 `AWAKE`: The robot reacts playfully to interaction — moving, making sounds, and animating facial expressions.
- 😠 `ANGRY`: Triggered by repetitive touches — the robot displays an angry expression and emits intense sounds.

These states transition depending on user interaction or inactivity.

## 🎮 Example Code Snippets

### 👆 Touch Response Logic

```cpp
if (lastButtonState == LOW && currentButtonState == HIGH) {
  switch (currentState) {
    case STATE_SLEEPING:
      currentState = STATE_WAKEUP;
      break;
    case STATE_BLINK:
      currentState = STATE_ANGRY;
      break;
  }
}

```
### 😠 Angry Eyes Display
```cpp
void angry_eyes() {
  display.clearDisplay();
  int tri_width = 40, tri_height = 35, center_y = 32;

  display.fillTriangle(21, center_y + tri_height / 2, 21, center_y - tri_height / 2, 21 + tri_width, center_y + tri_height / 2, SSD1306_WHITE);
  display.fillTriangle(107, center_y + tri_height / 2, 107, center_y - tri_height / 2, 107 - tri_width, center_y + tri_height / 2, SSD1306_WHITE);

  display.display();
}
```
### 🔊 Sound (Buzzer)
```cpp
void playBeep(int freq, int duration) {
  tone(BUZZER_PIN, freq);
  delay(duration);
  noTone(BUZZER_PIN);
}

void playRandomBeeps(int count) {
  for (int i = 0; i < count; i++) {
    playBeep(random(300, 1200), random(80, 150));
    delay(random(50, 150)); 
  }
}
```
