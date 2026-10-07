# F1 25 UDP LED Strip

> **DISCLAIMER**
>
> Enabling UDP Telemetry in F1 25 with the settings described in this guide caused my **Moza FSR steering wheel to stop receiving telemetry data**. I restored it by reconfiguring the game profile in the Moza app. With the current setup, you have to choose: either telemetry goes to your racing wheel, or this LED strip works. Both at the same time is not possible without additional configuration on your end.

---

## What does this do?

This project uses an ESP8266 microcontroller to receive live UDP telemetry from F1 25 and display race conditions on a NeoPixel LED strip.

| Condition | LED behaviour |
|---|---|
| Clear weather | Light yellow |
| Light cloud | Light blue |
| Overcast | White |
| Light rain | Light purple |
| Heavy rain | Purple |
| Storm | Dark purple |
| Safety car (full / virtual / formation) | Yellow blinking |
| Red flag | Red blinking (10 seconds) |

---

## Hardware requirements

- ESP8266 microcontroller (e.g. NodeMCU or Wemos D1 Mini)
- NeoPixel LED strip (WS2812B or compatible)
- USB-C cable (to upload the code to the ESP8266)
- Jumper wires to connect the LED strip to the ESP8266

![Hardware overview](read-me-images/hardware.jpg)

---

## Software requirements

- 2.4 GHz Wi-Fi network (the ESP8266 does not support 5 GHz)
- [Arduino IDE](https://www.arduino.cc/en/software)
- F1 25 (PC version, main game)

---

## Step 1 - Install the libraries

Two library ZIP files are included in the `libraries/` folder of this repository:

- `Adafruit_NeoPixel-master.zip`
- `f1-25-udp-main.zip`

To install them in Arduino IDE:

1. Open Arduino IDE.
2. Go to **Sketch** > **Include Library** > **Add .ZIP Library...**
3. Select `Adafruit_NeoPixel-master.zip` and click **Open**.
4. Repeat step 2 and 3 for `f1-25-udp-main.zip`.

![Library install](read-me-images/library-install.jpg)

---

## Step 2 - Download and open the code

1. In the `code_files/` folder of this repository, download `weather_and_safetycar_led.zip`.
2. Extract the ZIP file to a location of your choice.
3. Open Arduino IDE.
4. Go to **File** > **Open** and select the extracted `.ino` file.

![Open file](read-me-images/open-file.jpg)

---

## Step 3 - Configure the code

At the top of the file, change the following values to match your setup:

```cpp
const char *SSID     = "wifi-ssid";      // Name of your 2.4 GHz Wi-Fi network
const char *Password = "wifi-password";  // Your Wi-Fi password
```

```cpp
#define LED_PIN   5    // Change to D1 or another pin if needed
#define LED_COUNT 14   // Change to the number of LEDs on your strip
```

![Code configuration](read-me-images/code-config.jpg)

---

## Step 4 - Upload the code

1. Connect the ESP8266 to your computer using a USB-C cable.
2. In Arduino IDE, go to **Tools** > **Board** and select your ESP8266 board (e.g. **NodeMCU 1.0** or **LOLIN(WEMOS) D1 Mini**).
3. Go to **Tools** > **Port** and select the correct COM port.
4. Click the **Upload** button (arrow icon).

![Upload](read-me-images/upload.jpg)

---

## Step 5 - Configure F1 25

In F1 25, go to **Settings** > **Telemetry Settings** and apply the following:

| Setting | Value |
|---|---|
| UDP Telemetry | On |
| UDP Broadcast Mode | On |
| UDP Port | 20777 |

![F1 25 telemetry settings](read-me-images/f1-settings.jpg)

> See the disclaimer at the top of this README before changing these settings.

---

## Folder structure

```
f1_25_udp_ledstrip/
├── code_files/
│   └── weather_and_safetycar_led.zip
├── libraries/
│   ├── Adafruit_NeoPixel-master.zip
│   └── f1-25-udp-main.zip
├── read-me-images/
│   └── (images used in this README)
└── README.md
```
