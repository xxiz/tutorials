# Increasing Power Efficiency for HomeLab
A tutorial on decreasing power usage by a desktop computer running linux distros via `cpupower`
## Overview
### Specifications
* **OS:** Linux
### Versions
* **Ubuntu:** 22.04 LTS
## Steps
### Check CPU Powersave Governers
```bash
cpupower frequency-info
```
- This should return if there are powersave governers avaiable to control your CPU power frequencuy. Here is a sample output

![](https://f.1m.cx/B5uvpM58.png)
### Enabling Powersave Mode
```bash
cpupower frequency-set -g powersave
```
- This enables the powesave governer which runs the CPU at the minimum frequency as defined in `/sys/devices/system/cpu/cpuX/cpufreq/scaling_min_freq` (a list of included governers can be found [here](https://wiki.archlinux.org/title/CPU_frequency_scaling#Scaling_governors).)

### Checking power usage
There is currently no way to accuratley check the usage of watts by a computer and as such the only possible way currently is to purchase a wattmeter.
