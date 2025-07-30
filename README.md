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

### Touch Response Logic

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
<img width="421" height="365" alt="image" src="https://github.com/user-attachments/assets/a751b184-9a29-460a-90f5-d5d800f95b00" />
