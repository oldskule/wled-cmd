# wled-cmd

A simple, segment-aware command-line interface (CLI) for controlling [WLED](https://github.com/Aircoookie/WLED) devices via the JSON API.

Built for power users and automation scripts that want precise, programmable control of multi-segment WLED setups — including brightness tuning, effect changes, segment toggling, and proportional dimming/brightening.

---

# Changelog – wled-cmd

## v2.0 – Major Enhancements & Segment Brightness Control (2025-05-12)

### 🚀 New Features

- **Segment brightness scaling (`lighten` / `darken`)**  
  Added two new commands to scale brightness up or down by a given percentage:
  ```bash
  ./wled-cmd <ip> lighten 20%          # Decrease brightness of all segments by 20%
  ./wled-cmd <ip> darken 30% 0,1,2     # Increase brightness of segments 0,1,2 by 30%
  ```
  
- Soft Off using Brightness
- Replaced "on": false with "bri": 1 when turning segments off, ensuring segments stay logically on (especially for PWM setups).
- Preset Brightness into on Command
- The on command now sets segments to a brightness level of 150 by default.

---

## ✅ Improvements
- Robust fallback for segment brightness detection  
  If seg[].bri is unavailable, falls back to root .bri or uses 150 as a last resort.    
- Color Validation  
  Added a regex check to ensure set_color receives a valid 6-digit hex string ([0-9A-Fa-f]{6}).  
- Brightness Validation  
  set_brightness now checks that brightness is an integer between 0 and 255.  
- Percent Format Cleanup  
  Handles both 10 and 10% inputs in lighten/darken.  

---

## 🧹 Cleanups
- Standardized JSON payload construction for all segment-based operations
- Ensured all payload strings are properly quoted to avoid malformed requests
- Added support for segment iteration from 0–7 when no segment list is provided

---

## ✨ Features

- Control WLED using simple bash commands
- Full segment ID support (e.g. turn on/off specific lights)
- Adjust brightness up or down by percentage
- Cycle through effects (or set specific ones)
- Clean JSON-based API usage
- Graceful fallback support for systems without Bash ≥ 4.0

---

## 🛠 Requirements

Only two external dependencies are used:

- `curl` — for HTTP requests
- `xmllint` — for basic XML validation (rarely needed unless you extend the script)

### Install:

sudo apt-get install libxml2-utils

### Usage
```
./wled-cmd <ip-address> on                    # Sets all to level 150
./wled-cmd <ip-address> off  		      # Dims lights to least value
./wled-cmd <ip-address> status                # Get Status of LEDs
./wled-cmd <ip-address> brightness 128        # Adjusts Master Brightness Level
./wled-cmd <ip-address> set_effect 68         # Set Effects
./wled-cmd <ip-address> cycle		      # Cycle Effects
```

### Segment Control

```
./wled-cmd <ip-address> on 2,3,4             # Turn on segments 2, 3, and 4
./wled-cmd <ip-address> off 0,1,5            # Dim segments 0, 1, and 5 to "off"
./wled-cmd <ip-address> set_effect 10 1,2,3,4,5
```


### Brightness Tuning of Individual Segments by Percentage
```
./wled-cmd <ip-address> lighten 2,3,4 20%  # Decrease brightness of segments 2,3,4 by 20%
./wled-cmd <ip-address> lighten 20%        # Decrease all segments by 20%
./wled-cmd <ip-address> darken 0,1,5 30%   # Increase brightness of segments 0,1,5 by 30%
./wled-cmd <ip-address> darken 10%         # Increase all segments by 10%
```
