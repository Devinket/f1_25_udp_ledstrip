# F1 25 Weather Strip — ESP8266 + NeoPixel

Connect your F1 25 game to a LED strip via an ESP8266. The strip automatically reacts to the weather in your race: clear, rain, storm — the colour adjusts accordingly.

---

## What do you need?

| Hardware | Software |
|---|---|
| ESP8266 (e.g. NodeMCU) | Arduino IDE |
| NeoPixel LED strip (14 LEDs) | [f1-26-udp library](https://github.com/MacManley/f1-26-udp) |
| USB cable | Adafruit NeoPixel library |
| WiFi network (same as your PC) | F1 25 (PC) |

---

## Step 1 — Install libraries

1. Open the **Arduino IDE**
2. Go to **Sketch → Include Library → Manage Libraries**
3. Search for `Adafruit NeoPixel` and click **Install**
4. Download the [f1-26-udp library from GitHub](https://github.com/MacManley/f1-26-udp) as a ZIP file
5. Go to **Sketch → Include Library → Add .ZIP Library** and select the downloaded file

---

## Step 2 — Connect the hardware

Connect the NeoPixel LED strip to the ESP8266:

```
NeoPixel DATA  →  D1 (GPIO 5)
NeoPixel VCC   →  3.3V or 5V
NeoPixel GND   →  GND
```
![This is supposed to be a picture of the circuit](read-me-images/image.png)

> Note: With more than ~10 LEDs at full brightness, use an external 5V power supply for the strip.

---

## Step 3 — Upload the code

Download the Arduino file "f1code" and open it in the Arduino App.


Upload the code via **Sketch → Upload**.

---

## Step 4 — Configure F1 25

1. Open F1 25
2. Go to **Settings → Telemetry Settings**
3. Configure the following:

| Setting | Value |
|---|---|
| UDP Telemetry | **On** |
| Broadcast Mode | **On** |
| UDP Port | **20777** |
| UDP Format | **2025** |
| Send Rate | **20 Hz** |

> Note: With Broadcast Mode enabled, you don't need to enter an IP address — the ESP8266 will receive the data automatically as long as it's on the same WiFi network.

---

## Step 5 — Verify it works

1. Connect the ESP8266 via USB
2. Open the **Serial Monitor** in Arduino IDE (baud rate: `115200`)
3. The IP address will appear once the ESP8266 is connected to WiFi
4. Start a race in F1 25
5. The Serial Monitor will show `Weather: 0` (or another number)
6. The LED strip changes colour based on the weather in your race

---

## Weather values and colours

| Value | Weather | LED colour |
|---|---|---|
| `0` | Clear | Warm yellow |
| `1` | Light cloud | Light gray |
| `2` | Overcast | Dark gray |
| `3` | Light rain | Light blue |
| `4` | Heavy rain | Dark blue |
| `5` | Storm | Purple |

---

## Troubleshooting

**The strip does nothing:**
- Check that the DATA cable is connected to `D1`
- Make sure `NUM_LEDS` matches the number of LEDs on your strip

**Serial Monitor shows no weather data:**
- Make sure F1 25 and the ESP8266 are on the same WiFi network
- Ensure Broadcast Mode is set to **On** in F1 25
- Check that port `20777` is not blocked by a firewall

**WiFi won't connect:**
- Double-check your SSID and password in the code
- The ESP8266 only supports **2.4 GHz** WiFi, not 5 GHz

---

## File structure

```
project/
├── f1_weather_strip/
│   └── f1_weather_strip.ino   <- Arduino code
├── libraries/
│   ├── f1-26-udp/             <- UDP parser library
│   └── Adafruit_NeoPixel/     <- LED library
└── README.md                  <- This file
```

---

## Sources

- [f1-26-udp library (GitHub)](https://github.com/MacManley/f1-26-udp)
- [EA UDP Specification F1 25](https://forums.ea.com/blog/f1-games-game-info-hub-en/ea-sports%E2%84%A2-f1%C2%AE25-udp-specification/12187347)
- [Adafruit NeoPixel documentation](https://learn.adafruit.com/adafruit-neopixel-uberguide)
