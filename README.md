<p align="center"><img alt="Logo" src="images/logo.svg"></p>
<hr>
<h4 align="center">When xbacklight doesn't want to collaborate</h4>
<p align="center"><img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/giuseppe998e/bbacklight/Shellcheck?style=flat-square">  <img alt="GitHub" src="https://img.shields.io/github/license/giuseppe998e/bbacklight?style=flat-square"></p>
<br>

`bbacklight` is a command line utility, written in the POSIX shell language, created to overcome the problem of the more famous `xbacklight` which on some devices does not work as it should.  
This is why `bbacklight` was written trying to keep compatibility with `xbacklight` as much as possible.  

<br>

## Dependencies
Only GNU `coreutils`


## Installation
### Prerequisite
```shell
$ sudo groupadd bbacklight
$ echo "ACTION==\"add\", SUBSYSTEM==\"backlight\", KERNEL==\"<device>\", RUN+=\"/bin/chgrp bbacklight /sys/class/backlight/%k/brightness\"" | sudo tee -a /etc/udev/rules.d/bbacklight.rules
$ echo "ACTION==\"add\", SUBSYSTEM==\"backlight\", KERNEL==\"<device>\", RUN+=\"/bin/chmod g+w /sys/class/backlight/%k/brightness\"" | sudo tee -a /etc/udev/rules.d/bbacklight.rules
$ sudo usermod -aG bbacklight $USER
$ sudo udevadm control --reload-rules && sudo udevadm trigger # or reboot
```
Where `<device>` should be replaced with the device you want to use (ex. `acpi_video0` or `intel_backlight`).

### Git
```shell
$ curl -L "https://git.io/bbacklight" > bbacklight && chmod +x bbacklight
$ sudo mv bbacklight /usr/bin/
```


## Usage
```
$ bbacklight -help
Usage: bbacklight <command>
  where <command> are:
  -help
      Show this help text
  -version
      Show version
  -get [raw]
      Show the current brightness percentage (rounded down)
      If 'raw' is provided, it shows current brightness value
  -inv <percentage> (w/o % symbol)
      Increase the brightness by a percentage value decided by the user
  -dec <percentage> (w/o % symbol)
      Decrease the brightness by a percentage value decided by the user
  -set <percentage> (w/o % symbol)
      Set the brightness to a percentage value decided by the user
  -d <device>
      Choose which device to change the brightness or request the current value
      Default device is 'acpi_video0'
```
