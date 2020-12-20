<p align="center">
  <a href="#readme">
    <img alt="Logo" src="images/logo.svg">
  </a>
</p>
<hr>
<h4 align="center">When xbacklight doesn't want to collaborate</h4>
<p align="center">
  <a href="https://github.com/giuseppe998e/bbacklight/actions?query=workflow%3AShellcheck">
    <img alt="GitHub Workflow Status" src="https://img.shields.io/github/workflow/status/giuseppe998e/bbacklight/Shellcheck?style=flat-square">
  </a> 
  <a href="https://github.com/giuseppe998e/bbacklight/blob/main/LICENSE">
    <img alt="GitHub License" src="https://img.shields.io/github/license/giuseppe998e/bbacklight?style=flat-square">
  </a> 
  <a href="#installation">
    <img alt="GitHub Latest Tag" src="https://img.shields.io/github/v/tag/giuseppe998e/bbacklight?style=flat-square">
  </a>
</p>
<br>

`bbacklight` is a command line utility, written in the POSIX shell language, created to overcome the problem of the more famous `xbacklight` which on some devices does not work as it should.  
This is why `bbacklight` was written trying to keep compatibility with `xbacklight` as much as possible.  


## Dependencies
- `gnu-coreutils` or `busybox`
- `curl` or `wget` (*optional*)


## Installation
### Prerequisite
```console
$ sudo groupadd bbacklight
$ echo "ACTION==\"add\", SUBSYSTEM==\"backlight\", KERNEL==\"<device>\", RUN+=\"/bin/chgrp bbacklight /sys/class/backlight/%k/brightness\"" | sudo tee -a /etc/udev/rules.d/bbacklight.rules
$ echo "ACTION==\"add\", SUBSYSTEM==\"backlight\", KERNEL==\"<device>\", RUN+=\"/bin/chmod g+w /sys/class/backlight/%k/brightness\"" | sudo tee -a /etc/udev/rules.d/bbacklight.rules
$ sudo usermod -aG bbacklight $USER
$ sudo udevadm control --reload-rules && sudo udevadm trigger # or reboot
```
Where `<device>` should be replaced with the device you want to use (ex. `acpi_video0` or `intel_backlight`).

### Git
```console
$ curl -L "https://git.io/bbacklight" > bbacklight && chmod +x bbacklight
$ sudo mv bbacklight /usr/bin/
```


## Configuration
The program is set by default to use the first entry in the `/sys/class/backlight` directory.  
To change this behavior, edit the program with a text editor, setting the `DEF_DEVICE` variable with an entry/device of your choice (ex.`DEF_DEVICE="acpi_video0"` Or `DEF_DEVICE="intel_backlight"`).  
Otherwise you can use the `-d <DEVICE>` option.


## Usage
```console
$ bbacklight -help
Usage: bbacklight <command>
  where <command> are:
  -help
      Show this help text
  -version
      Show version
      And, possibly, if a different version is available on GitHub
  -get [raw]
      Show the current brightness percentage (rounded down)
      If 'raw' is provided, it shows the current brightness value
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
