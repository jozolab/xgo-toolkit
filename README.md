# xgo-toolkit

A modified version of [XGO-PythonLib](https://github.com/Xgorobot/XGO-PythonLib/), aim to support recent Raspberry Pi OS (bookworm) on XGO-Rider / Rider-Pi, and to have more options for usage.

## XGO-PythonLib

XGO2 has built-in motion libraries for controlling the movement and various features of the machine dog, including battery level, firmware version, and servo angle. The motion library enables users to control translation and pose movement, as well as single servo and single-leg movement. The education library facilitates camera, screen, key, microphone, and speaker operations, as well as commonly used AI functions such as gesture recognition, face detection, emotional recognition, and age and gender recognition.  The detailed instructions for use of the library are as follows.

PythonLib included xgolib.py and xgoedu.py

[Luwu Dynamics · WIKI](https://www.yuque.com/luwudynamics)


## Install instructions 

1. Burn the latest Raspberry Pi OS Lite (64-bit, Debian bookworm) with [rpi-imager](https://www.raspberrypi.com/software/), ensure you have set up Wi-Fi, hostname (e.g. `rpi4-dev`) and login (e.g. `pi`).

2. Plug the sdcard to XGO-Rider, and connect it via ssh
```shell
ssh pi@rpi4-dev
```

3. Install following system packages for building sound card support

```shell
sudo apt install git build-essential linux-headers-rpi-v8
```

4. Setup soundcard driver

```shell
cd ~
git clone https://github.com/jozolab/WM8960-Audio-HAT-bookworm
cd WM8960-Audio-HAT-bookworm
sudo ./install.sh 
```

5. Install required python libraries and packages

```shell
sudo apt install mplayer python3-serial python3-opencv python3-pil python3-pip
```

6. Run this library to system:

```
sudo pip install --upgrade xgo-toolkit --break-system-packages
```

7. Reboot
```shell
sudo reboot
```

## Examples

Perform gesture recognition on the current camera and press the "c" key to exit.

```python
from xgo_toolkit import XGOEDU 
XGO_edu = XGOEDU()

while True:
    result=XGO_edu.gestureRecognition()  
    print(result)
    if XGO_edu.xgoButton("c"):  
        break
```
XGO library example
```python
from xgo_toolkit import XGO
dog = XGO('xgorider')
dog.action(1)
```
## Change Log

### [0.1.6] - 2025-01-05

- Forked from original [0.3.5] to xgo-toolkit [0.1.6]
- add auto download files in model to home directory
- Remove all hardcoded path in XGOEDU
- Refactor files to a single module