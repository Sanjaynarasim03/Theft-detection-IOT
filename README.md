# ESP32-CAM Telegram Motion Camera 🚀

A home surveillance system using the ESP32-CAM module that sends real-time photos to a Telegram bot when motion is detected or on-demand via chat commands.

---

## 📋 Features

* **Motion Detection**: PIR sensor triggers photo capture and sends to Telegram.
* **On-Demand Photos**: Send `/photo` or `/photoWithFlash` commands to the bot to receive snapshots.
* **Flash Control**: Optional LED flash for low-light conditions.
* **Secure Connection**: HTTPS requests to Telegram API via `WiFiClientSecure`.
* **Buzzer Alert**: Audible indication when motion is detected.

---

## 🔧 Hardware & Wiring

| Component         | ESP32-CAM GPIO | Notes                     |
| ----------------- | -------------- | ------------------------- |
| ESP32-CAM module  | -              | AI-Thinker board          |
| PIR Motion Sensor | GPIO 13 (PIR)  | `PIR`                     |
| Flash LED         | GPIO 4 (FLASH) | `FLASH_LED`               |
| Buzzer            | GPIO 12        | `BUZZER_PIN`              |
| 3.3V & GND        | 3.3V, GND      | Power to sensors & buzzer |

> **ESP32-CAM pinout** is preconfigured for AI-Thinker variant. Adjust `camera_config_t` if using different modules.

---

## 🔌 Software Dependencies

* **Arduino IDE** or PlatformIO
* **Libraries** (install via Library Manager or PlatformIO):

  * `WiFi.h` & `WiFiClientSecure.h` (built-in)
  * `esp_camera.h` (ESP32-CAM support)
  * `UniversalTelegramBot`
  * `ArduinoJson`
  * `DHT` (if enabling temperature/humidity)

---

## ⚙️ Configuration

1. **Wi-Fi Credentials**

   ```cpp
   const char* ssid     = "<YOUR_WIFI_SSID>";
   const char* password = "<YOUR_WIFI_PASSWORD>";
   ```

2. **Telegram Bot**

   * Create a bot via @BotFather and note the **Bot Token**.
   * Start the bot in Telegram to get a **Chat ID** (use @myidbot).

   ```cpp
   String BOTtoken = "<YOUR_BOT_TOKEN>";
   String chatId   = "<YOUR_CHAT_ID>";
   ```

3. **Motion Sensor & Flash**

   * Set `motionSensorFlag = true;` via `/motionOn` command.
   * Enable flash via `/photoWithFlash` command.

---

## 📥 Installation & Upload

1. **Install ESP32 Board**

   * In Arduino IDE: **File > Preferences**
   * Add `https://dl.espressif.com/dl/package_esp32_index.json` to **Additional Boards Manager URLs**
   * Open **Tools > Board > Boards Manager**, search **esp32**, install **ESP32 by Espressif Systems**

2. **Select Board & Settings**

   * **Board**: `AI Thinker ESP32-CAM`
   * **Upload Speed**: `115200`
   * **Flash Frequency**: `40MHz`
   * **Partition Scheme**: `Huge APP (3MB No OTA)` (or default)

3. **Wire Components**

   * Connect PIR, flash LED, buzzer as per wiring table.

4. **Flash Code**

   * Compile and upload the sketch to ESP32-CAM.
   * Open Serial Monitor at `115200` baud to view IP and debug logs.

---

## 📡 Usage

* **Start Bot**: Send `/start` in Telegram to see available commands.
* **On-Demand Photo**: `/photo`, `/photoWithFlash`
* **Enable/Disable Motion**: `/motionOn`, `/motionOff`
* **Motion Alerts**: When motion is detected, the device sends a photo and toggles the buzzer.

---

## 🛠️ Troubleshooting

* **Camera Init Failed**: Check wiring, ensure correct board selected, enable PSRAM if prompted.
* **No Wi-Fi**: Verify SSID/password, router settings (2.4GHz only).
* **No Telegram Messages**: Confirm BOT token, chat ID, and that you pressed *Start* in bot.
* **Flash Always On**: Ensure `withFlash` toggles off after use.

---

## 🙌 Contributions

Feel free to fork, submit issues, or pull requests to add features like:

* Face recognition
* Cloud storage of images
* Additional sensor data (temperature, humidity)

---

## 📜 License

[MIT License](LICENSE)

---

*Created by Sanjay Narasimhan, July 2025*
