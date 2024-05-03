#!/bin/bash
usage() {
  echo "Usage: $0 ipaddress {on|off|get_brightness|set_brightness|set_color|cycle|set_effect|status}"
}

# Validate IP address
if [[ $1 =~ ^(([1-9]?[0-9]|1[0-9][0-9]|2([0-4][0-9]|5[0-5]))\.){3}([1-9]?[0-9]|1[0-9][0-9]|2([0-4][0-9]|5[0-5]))$ ]]; then
  ip=$1
else
  echo "Missing or invalid IP address"
  usage
  exit 1
fi

# Function to parse HTTP codes
http_code() {
  local code="$1"
  case "$code" in
    "200") echo "Success ($code)";;
    "400") echo "Bad Request ($code)";;
    "404") echo "Not Found ($code)";;
    *) echo "HTTP Code $code";;
  esac
}

# Turn WLED on
on() {
  JSON_PAYLOAD='{"on": true}'
  return=$(curl -s -o /dev/null -w "%{http_code}\n" -H "Content-Type: application/json" -d "$JSON_PAYLOAD" "http://$ip/json/state")
  http_code $return
}

# Turn WLED off
off() {
  JSON_PAYLOAD='{"on": false}'
  return=$(curl -s -o /dev/null -w "%{http_code}\n" -H "Content-Type: application/json" -d "$JSON_PAYLOAD" "http://$ip/json/state")
  http_code $return
}

# Get brightness
get_brightness() {
  curl -s "http://$ip/json/state" | jq '.bri'
}

# Set brightness
set_brightness() {
  local brightness=$1
  if [[ ! "$brightness" ]]; then
    brightness_help
    exit 1
  fi
  JSON_PAYLOAD="{\"bri\":$brightness}"
  return=$(curl -s -o /dev/null -w "%{http_code}\n" -H "Content-Type: application/json" -d "$JSON_PAYLOAD" "http://$ip/json/state")
  http_code $return
}

# Set color
set_color() {
  local color=$1
  if [[ ! "$color" ]]; then
    color_help
    exit 1
  fi
  # Convert hex color to decimal RGB values
  r=$(printf '%d' "0x${color:0:2}")
  g=$(printf '%d' "0x${color:2:2}")
  b=$(printf '%d' "0x${color:4:2}")
  JSON_PAYLOAD="{\"seg\":{\"col\":[[$r,$g,$b]]}}"
  return=$(curl -s -o /dev/null -w "%{http_code}\n" -H "Content-Type: application/json" -d "$JSON_PAYLOAD" "http://$ip/json/state")
  http_code $return
}

# Cycle colors/effects
cycle() {
  echo "Cycle functionality needs to be customized based on available API operations."
}

# Set effect
set_effect() {
  local effect=$1
  if [[ ! "$effect" ]]; then
    fx_help
    exit 1
  fi
  JSON_PAYLOAD="{\"seg\":{\"fx\":$effect}}"
  return=$(curl -s -o /dev/null -w "%{http_code}\n" -H "Content-Type: application/json" -d "$JSON_PAYLOAD" "http://$ip/json/state")
  http_code $return
}
  
# Display current status
status() {
  curl -s "http://$ip/json/state"
  echo
}

# Helper functions for input
brightness_help() {
  echo "brightness requires a 3rd argument specifying the brightness between 0 and 255"
} 

color_help() {
  echo "set_color requires a 3rd argument specifying the color in RGB hexadecimal format (e.g., FF00FF)"
}
  
fx_help() {
  echo "set_effect requires a 3rd argument specifying the effect number"
}
    
# Process commands
case "$2" in
    on) on;;
    off) off;;
    get_brightness) get_brightness;;
    set_brightness) set_brightness $3;;
    set_color) set_color $3;;
    cycle) cycle $3 $4 &;;
    set_effect) set_effect $3;;
    status) status;;
    *) echo "Invalid command"; usage;;
esac   
  
  
