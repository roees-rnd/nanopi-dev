# nanopi-dev

### hooking up:
#### 2. iniate a wifi connection:

With commandline Utility (nmcli) Check WiFi:

##### a. Check Device List
```
$ sudo nmcli dev
```
*Note*: if a device's status is unmanaged it means this device is not accessed by the NetworkManager and you need to clear the settings under /etc/network/interfaces and reboot.

##### b. Start WiFi
```
$ sudo nmcli r wifi on
```
##### c. Scan Surrounding WiFi Hotspots
```
$ sudo nmcli dev wifi
```
##### d. Connect to WiFi Hotspot
```
$ sudo nmcli dev wifi connect "SSID" password "PASSWORD"
```


### installations
#### 1. cmake
Download source code:
```
wget https://github.com/Kitware/CMake/releases/download/v3.17.2/cmake-3.17.2.tar.gz
```
unzip and build:
```
tar -xzf cmake-3.17.2.tar.gz
cd cmake-3.17.2/
./bootstrap && make && sudo make install
```
