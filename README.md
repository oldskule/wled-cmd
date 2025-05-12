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
./wled-cmd <ip-address> on  
./wled-cmd <ip-address> off  
./wled-cmd <ip-address> status  
./wled-cmd <ip-address> brightness 128  
./wled-cmd <ip-address> set_effect 68  
./wled-cmd <ip-address> cycle
```

### Segment Control

```
./wled-cmd <ip-address> on 2,3,4      # Turn on segments 2, 3, and 4
./wled-cmd <ip-address> off 0,1,5     # Dim segments 0, 1, and 5 to "off"
./wled-cmd <ip-address> set_effect 10 1,2,3,4,5
```


### Brightness Tuning by Percentage
```
./wled-cmd <ip-address> lighten 2,3,4 20%  # Decrease brightness of segments 2,3,4 by 20%
./wled-cmd <ip-address> lighten 20%        # Decrease all segments by 20%
./wled-cmd <ip-address> darken 0,1,5 30%   # Increase brightness of segments 0,1,5 by 30%
./wled-cmd <ip-address> darken 10%         # Increase all segments by 10%
```
