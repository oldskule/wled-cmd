# wled-cmd
Simple command line interface for WLED devices.

- Forked from mplinuxgeek/wled-cmd, props to GPT
- Updated to use JSON API.
- Fixed errors thrown when bash not >= 4.0

# requirements
There are only 2 tools called by this script:
curl
xmllint
- Fedora: dnf install libxml2
- Ubuntu: apt-get install libxml2-utils

# usage
```
./wled-cmd 192.168.1.147 on
./wled-cmd 192.168.1.147 brightness 128
./wled-cmd 192.168.1.147 cycle (this one cycles through a list of effects in the script)
./wled-cmd 192.168.1.147 fx 68
./wled-cmd 192.168.1.147 status
./wled-cmd 192.168.1.147 off

./wled-cmd 192.168.1.147 off [comma_separated_list_of_segment_ids]
./wled-cmd 192.168.1.147 on [comma_separated_list_of_segment_ids]
```
