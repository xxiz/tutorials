# Deattaching Terminals in Linux (screen/tmux)
A tutorial on deattaching terminals in Linux to allow you to close your terminal without killing your processes.
## Overview
### Specifications
* **OS:** Linux
### Versions
* **Ubuntu:** 22.04 LTS
* **screen:** 4.9.0
* **tmux:** 3.2a
## Steps (Screen)
### Installing screen
install screen by running
```bash
sudo apt install screen
```
### Using screen
start a new screen session by running
```bash
screen
```
On the first run you will be prompted with a message asking you to agree to the terms of screen. You can continue by pressing `return`.

You will now be in a new screen session. You can now run any commands you want. To exit the screen session, press `ctrl+a` followed by `d`. This will detach you from the screen session. You can now close your terminal while your program runs in the background.

To reattach to the screen session, first the command below to view all active screen sessions.
```bash
screen -list
```
You will see a list of all active screen sessions. You can now reattach to the screen session by running
```bash
screen -r <session name>
```

## Steps (tmux)
> Note: Since tmux comes preinstalled on Ubuntu 22.04, you do not need to install it.

### Using tmux
start a new tmux session by running
```bash
tmux
```
You will now be in a new tmux session. You can now run any commands you want. To exit the tmux session, press `ctrl+b` followed by `d`. This will detach you from the tmux session. You can now close your terminal while your program runs in the background.

To reattach to the tmux session, first the command below to view all active tmux sessions.
```bash
tmux ls
```
You will see a list of all active tmux sessions. You can now reattach to the tmux session by running
```bash
tmux a -t <session name>
```