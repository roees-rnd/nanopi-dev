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
#### 1. cmake (didnt work)
Download source code:
```shell
wget https://github.com/Kitware/CMake/releases/download/v3.17.2/cmake-3.17.2.tar.gz
```
unzip and build:
```shell
tar -xzf cmake-3.17.2.tar.gz
cd cmake-3.17.2/
./bootstrap && make && sudo make install
```
THIS WAY FAILED ME ...

#### 2. cmake workaround - cross-compiling
This means using cmake and gcc on pc (e.g. intel x86) to compile for target (arm). I followed this guys [link](https://medium.com/@au42/the-useful-raspberrypi-cross-compile-guide-ea56054de187) to get the basic idea. I had to change qute alot to get it to work with our the nanopi.

In short:
First on your computer create a dev folder (~/projects/dev_tools/friendlyArm_toolchain) download and extract toolchain file `arm-cortexa9-linux-gnueabihf-4.9.3-20160512.tar.xz` from [google drive of friendlyArm](https://drive.google.com/drive/folders/15yJCIVY2A3_lk4H0NEoN-EteLR_umKFD) to new the directory.

in dev_tools create a cmake file named `cross_compile_nanopi.cmake` containing:
```cmake
# Define our host system
SET(CMAKE_SYSTEM_NAME Linux)
SET(CMAKE_SYSTEM_VERSION 1)
# Define the cross compiler locations
SET(CMAKE_C_COMPILER   "/home/roee/projects/dev_tools/friendlyArm_toolchain/4.9.3/bin/arm-cortexa9-linux-gnueabihf-gcc")

SET(CMAKE_CXX_COMPILER "/home/roee/projects/dev_tools/friendlyArm_toolchain/4.9.3/bin/arm-cortexa9-linux-gnueabihf-gcc")

# Define the sysroot path for the RaspberryPi distribution in our tools folder 
SET(CMAKE_FIND_ROOT_PATH CMAKE_CXX_COMPILER "/home/roee/projects/dev_tools/friendlyArm_toolchain/4.9.3/arm-cortexa9-linux-gnueabihf/sys-root/")
SET(CMAKE_FIND_ROOT_PATH CMAKE_C_COMPILER "/home/roee/projects/dev_tools/friendlyArm_toolchain/4.9.3/arm-cortexa9-linux-gnueabihf/sys-root/")

# Use our definitions for compiler tools
SET(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
# Search for libraries and headers in the target directories only
SET(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
SET(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)

add_definitions(-Wall -std=c11)
```





