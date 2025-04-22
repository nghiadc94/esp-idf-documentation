# Espressif ESP-IDF Documentation

This document provides a step-by-step guide to set up and use the Espressif IoT Development Framework (ESP-IDF) for developing firmware on ESP32 microcontrollers.

## Table of Contents
1. [Requirement](#requirements)
2. [Installation](#installation)
    - [Windows](#windows)
    - [Linux](#linux)
    - [MacOS](#macos)
3. [Environment Setup](#environment-setup)
4. [Creating a New Project](#creating-a-new-project)
5. [Configure a Project](#configure-a-project)
6. [Compiling and Flashing](#compiling-and-flashing)
7. [Common Commands](#common-commands)
8. [Project Structure](#project-structure)
9. [Useful Tips](#useful-tips)

## Requirements
1. The installer of ESP-IDF deploys the following components:
  * Embedded Python
  * Cross-compilers
  * OpenOCD
  * [CMake](https://cmake.org/download/) and [Ninja](https://ninja-build.org/) build tools
  * ESP-IDF
2. USB-to-Serial drivers for ESP32 (CP210x, FTDI, or CH340) (included with ESP32 Dev Board)

## Installation

### Windows
1. Download the ESP-IDF Tools Installer (newest version 5.4.1) from: https://dl.espressif.com/dl/esp-idf
   ![image](https://github.com/user-attachments/assets/931557e2-1096-4834-a5cb-caf3f090a7bc)

3. Run the offline installer. Offline Installer does not require any network connection, it contains all required dependencies including [Git For Windows](https://gitforwindows.org/).
4. The installer stores downloaded files in the cache directory `%userprofile%\.espressif`
5. The installer also allows reusing the existing directory with ESP-IDF. The recommended directory is `%userprofile%\Desktop\esp-idf` where `%userprofile%` is your home directory.
6. At the end of the installation process you can check out option `Run ESP-IDF PowerShell Environment` or `Run ESP-IDF Command Prompt (cmd.exe)`. The installer launches ESP-IDF environment in selected prompt.
   * `Run ESP-IDF PowerShell Environment`
     ![image](https://github.com/user-attachments/assets/d299c160-ed51-4d24-b03d-fdff7ff23fbe)
     ![image](https://github.com/user-attachments/assets/379dca0c-4d22-410c-896b-cd972e2f1135)

   * `Run ESP-IDF Command Prompt (cmd.exe)`
     ![image](https://github.com/user-attachments/assets/ae5c633b-ea73-48d8-bccc-9969d7b70e6f)
     ![image](https://github.com/user-attachments/assets/be14fd1d-3a78-4b47-a85d-2cdf889787df)

### Linux
These are the steps for setting up the ESP-IDF for your ESP32.
- Install Prerequisites
- Get ESP-IDF
- Set up the Tools

1. Install prerequisites:
   - Ubuntu and Debian:
     ```
     sudo apt-get install git wget flex bison gperf python3 python3-pip python3-venv cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0
     ```
   - CentOS 7 & 8:
     ```
     sudo yum -y update && sudo yum install git wget flex bison gperf python3 cmake ninja-build ccache dfu-util libusbx
     ```
   - Arch:
     ```
     sudo pacman -S --needed gcc git make flex bison gperf python cmake ninja ccache dfu-util libusb python-pip
     ```
     
2. Get ESP-IDF
    - To build applications for the ESP32, you need the software libraries provided by Espressif in [ESP-IDF repository](https://github.com/espressif/esp-idf).
    - To get ESP-IDF, navigate to your installation directory and clone the repository with git clone, following instructions below specific to your operating system.
    - Open Terminal, and run the following commands:
      ```
      mkdir -p ~/esp
      cd ~/esp
      git clone --recursive https://github.com/espressif/esp-idf.git
      ```
    - ESP-IDF is downloaded into `~/esp/esp-idf`
    - Consult [ESP-IDF Versions](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/versions.html) for information about which ESP-IDF version git.

3. Set up the Tools
    - Aside from the ESP-IDF, you also need to install the tools used by ESP-IDF, such as the compiler, debugger, Python packages, etc, for projects supporting ESP32.
      ```
      cd ~/esp/esp-idf
      ./install.sh esp32
      ```
      or with Fish shell
      ```
      cd ~/esp/esp-idf
      ./install.fish esp32
      ```
    - The above commands install tools for ESP32 only. If you intend to develop projects for more chip targets then you should list all of them and run for example:
      ```
      cd ~/esp/esp-idf
      ./install.sh esp32,esp32s2
      ```
      or with Fish shell
      ```
      cd ~/esp/esp-idf
      ./install.fish esp32,esp32s2
      ```
    - In order to install tools for all supported targets please run the following command:
      ```
      cd ~/esp/esp-idf
      ./install.sh all
      ```
      or with Fish shell
      ```
      cd ~/esp/esp-idf
      ./install.fish all
      ```
    - Alternative File Downloads: If accessing GitHub is slow then it is possible to set an environment variable to prefer Espressif's download server for GitHub asset downloads. To prefer the Espressif download server when installing tools, use the following sequence       of commands when running install.sh:
      ```
      cd ~/esp/esp-idf
      export IDF_GITHUB_ASSETS="dl.espressif.com/github_assets"
      ./install.sh
      ```
    - Customizing the Tools Installation Path: The scripts introduced in this step install compilation tools required by ESP-IDF inside the user home directory: `$HOME/.espressif` on Linux. If you wish to install the tools into a different directory, export the              environment variable IDF_TOOLS_PATH before running the installation scripts. Make sure that your user account has sufficient permissions to read and write this path.
      ```
      export IDF_TOOLS_PATH="$HOME/required_idf_tools_path"
      ./install.sh

      . ./export.sh
      ```
      If changing the `IDF_TOOLS_PATH`, make sure it is exported in the environment before running any ESP-IDF tools or scripts. **Note:** Using `IDF_TOOLS_PATH` in variable assignment, e.g., `IDF_TOOLS_PATH="$HOME/required_idf_tools_path" ./install.sh`, without prior exporting, will not work in most shells because the variable assignment will not affect the current execution environment, even if it's exported/changed in the sourced script.
For more details and error resolving, consult [ESP-IDF Setup for MacOS](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html#get-started-get-esp-idf).
### MacOS
These are the steps for setting up the ESP-IDF for your ESP32.
- Install Prerequisites
- Get ESP-IDF
- Set up the Tools

1. Install prerequisites:
    - ESP-IDF uses the version of Python installed by default on macOS.
    - Install CMake & Ninja build:
      * If you have [HomeBrew](https://brew.sh/), you can run:
        ```
        brew install cmake ninja dfu-util
        ```
      * If you have [MacPorts](https://www.macports.org/install.php), you can run:
        ```
        sudo port install cmake ninja dfu-util
        ```
      * Otherwise, consult the [CMake](https://cmake.org/) and [Ninja](https://ninja-build.org/) home pages for macOS installation downloads.
    - It is strongly recommended to also install [ccache](https://ccache.dev/) for faster builds. If you have **HomeBrew**, this can be done via `brew install ccache` or `sudo port install ccache` on **MacPorts**.

2. Get ESP-IDF
    - To build applications for the ESP32, you need the software libraries provided by Espressif in [ESP-IDF repository](https://github.com/espressif/esp-idf).
    - To get ESP-IDF, navigate to your installation directory and clone the repository with git clone, following instructions below specific to your operating system.
    - Open Terminal, and run the following commands:
      ```
      mkdir -p ~/esp
      cd ~/esp
      git clone --recursive https://github.com/espressif/esp-idf.git
      ```
    - ESP-IDF is downloaded into `~/esp/esp-idf`
    - Consult [ESP-IDF Versions](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/versions.html) for information about which ESP-IDF version git.
3. Set up the Tools
    - Aside from the ESP-IDF, you also need to install the tools used by ESP-IDF, such as the compiler, debugger, Python packages, etc, for projects supporting ESP32.
      ```
      cd ~/esp/esp-idf
      ./install.sh esp32
      ```
      or with Fish shell
      ```
      cd ~/esp/esp-idf
      ./install.fish esp32
      ```
    - The above commands install tools for ESP32 only. If you intend to develop projects for more chip targets then you should list all of them and run for example:
      ```
      cd ~/esp/esp-idf
      ./install.sh esp32,esp32s2
      ```
      or with Fish shell
      ```
      cd ~/esp/esp-idf
      ./install.fish esp32,esp32s2
      ```
    - In order to install tools for all supported targets please run the following command:
      ```
      cd ~/esp/esp-idf
      ./install.sh all
      ```
      or with Fish shell
      ```
      cd ~/esp/esp-idf
      ./install.fish all
      ```
      
For more details and error resolving, consult [ESP-IDF Setup for MacOS](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html#get-started-get-esp-idf).
## Environment Setup

### Windows
- ESP-IDF Tools Installer already created a shortcut in the Start menu and Desktop for these 2 options to launch the ESP-IDF when installation is done. These shortcuts launch the corresponding environment and runs `export.bat` script to set up the environment            variables (`PATH`, `IDF_PATH` and others). Inside theses, all the installed tools are available.
- These shortcuts are specific to the ESP-IDF directory selected in the ESP-IDF Tools Installer. If you have multiple ESP-IDF directories on the computer (for example, to work with different versions of ESP-IDF), you have two options to use them:
  * Create a copy of the shortcut created by the ESP-IDF Tools Installer, and change the working directory of the new shortcut to the ESP-IDF directory you wish to use.
  * Alternatively, run `cmd.exe` or `powershell.exe`, then change to the ESP-IDF directory you wish to use, and run `export.bat`. Note that unlike the previous option, this way requires `Python` and `Git` to be present in `PATH`. If you get errors related to                `Python` or `Git` not being found, use the first option.
 
### Linux and MacOS
The installed tools are not yet added to the PATH environment variable. To make the tools usable from the command line, some environment variables must be set. ESP-IDF provides another script which does that.
- In the terminal where you are going to use ESP-IDF, run:
  ```
  . $HOME/esp/esp-idf/export.sh
  ```
  or for fish (supported only since fish version 3.0.0):
  ```
  . $HOME/esp/esp-idf/export.fish
  ```
- If you plan to use esp-idf frequently, you can create an alias for executing `export.sh`:
  * Copy and paste the following command to your shell's profile (`.profile`, `.bashrc`, `.zprofile`, etc.)
    ```
    alias get_idf='. $HOME/esp/esp-idf/export.sh'
    ```
  * Refresh the configuration by restarting the terminal session or by running `source [path to profile]`, for example, `source ~/.bashrc`.

Now you can run `get_idf` to set up or refresh the esp-idf environment in any terminal session.

Technically, you can add `export.sh` to your shell's profile directly; however, it is not recommended. Doing so activates IDF virtual environment in every terminal session (including those where IDF is not needed), defeating the purpose of the virtual environment and likely affecting other software.

## Creating a New Project

### Windows
You can start with [get-started/hello_world](https://github.com/espressif/esp-idf/tree/186f2a89/examples/get-started/hello_world) project from [examples](https://github.com/espressif/esp-idf/tree/186f2a89/examples) directory in ESP-IDF.
Copy the project [get-started/hello_world](https://github.com/espressif/esp-idf/tree/186f2a89/examples/get-started/hello_world) to `~/esp` directory, or use below commands:
```
cd %userprofile%\esp
xcopy /e /i %IDF_PATH%\examples\get-started\hello_world hello_world
```

### Linux and MacOS
You can start with [get-started/hello_world](https://github.com/espressif/esp-idf/tree/186f2a89/examples/get-started/hello_world) project from [examples](https://github.com/espressif/esp-idf/tree/186f2a89/examples) directory in ESP-IDF.
Copy the project [get-started/hello_world](https://github.com/espressif/esp-idf/tree/186f2a89/examples/get-started/hello_world) to `~/esp` directory:
```
cd ~/esp
cp -r $IDF_PATH/examples/get-started/hello_world .
```

## Configure a Project
ESP-IDF have a `menuconfig` for easy configure the feature of ESP32, automatically set up definition and feature which you can quickly use during the devolopment.

However, it is your choice to follow this or not. You can implement these settings by your own code.
![image](https://github.com/user-attachments/assets/d440f1f1-87af-46a2-9e1b-9d7266a25220)

After open ESP-IDF followed by previous steps, navigate to `your-project` directory, set ESP32 as the target, and run the project configuration utility `menuconfig`.
```
cd ~/esp/your-project
idf.py set-target esp32
idf.py menuconfig
```
Chip type will affect the `set-target` command. For detail, checkout [Select the Target Chip: set-target](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/tools/idf-py.html#selecting-idf-target).
For further infomration about `menuconfig`, run `idf.py menuconfig --help`

## Compiling and Flashing

### Build the Project
Build the project by running:
```
idf.py build
```
This command compiles the application and all ESP-IDF components, then it generates the bootloader, partition table, and application binaries.
```
$ idf.py build
Running cmake in directory /path/to/hello_world/build
Executing "cmake -G Ninja --warn-uninitialized /path/to/hello_world"...
Warn about uninitialized values.
-- Found Git: /usr/bin/git (found version "2.17.0")
-- Building empty aws_iot component due to configuration
-- Component names: ...
-- Component paths: ...

... (more lines of build system output)

[527/527] Generating hello_world.bin
esptool.py v2.3.1

Project build complete. To flash, run this command:
../../../components/esptool_py/esptool/esptool.py -p (PORT) -b 921600 write_flash --flash_mode dio --flash_size detect --flash_freq 40m 0x10000 build/hello_world.bin  build 0x1000 build/bootloader/bootloader.bin 0x8000 build/partition_table/partition-table.bin
or run 'idf.py -p PORT flash'
```
If there are no errors, the build finishes by generating the firmware binary .bin files.

### Flash onto the Device
**CP210x, FTDI, or CH340 and its driver are required for flashing** when come to custom ESP32 board. Make sure to add those module into the custom board. 
ESP32 can be flashed through UART0 pins which is connected to GPIO1 (TX) and GPIO3 (RX).

Connect your ESP32 board to the computer and check under which serial port the board is visible:

**Windows**: starting with `COM`

**Linux**: starting with `/dev/tty`

**MacOS**: starting with `/dev/cu.`

To flash the binaries that you just built for the ESP32 in the previous step, you need to run the following command:
```
idf.py -p PORT flash
```
Replace `PORT` with your ESP32 board's USB port name. If the `-p PORT` is not defined in command, the `idf.py` will try to connect automatically using the available USB ports.

If you are not sure how to check the serial port name, please refer to [Establish Serial Connection with ESP32](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/establish-serial-connection.html) for full details.
**Note**: The option flash automatically builds and flashes the project, so if you have plan to run/test immediately, idf.py build is not necessary.

**Flash Erase**
Erasing the flash is also possible. To erase the entire flash memory you can run the following command:
```
idf.py -p PORT erase-flash
```
For erasing the `OTA data` partition while working with OTA feature, you can run this command:
```
idf.py -p PORT erase-otadata
```

If there is any issues encountered during flashing, see the [Useful Tips](#useful-tips) below. You can also refer to [Flashing Troubleshooting](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/flashing-troubleshooting.html) page or [Establish Serial Connection with ESP32](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/establish-serial-connection.html) for more detailed information.

When flashing, there is output log similar to the following:
```
...
esptool.py --chip esp32 -p /dev/ttyUSB0 -b 460800 --before=default_reset --after=hard_reset write_flash --flash_mode dio --flash_freq 40m --flash_size 2MB 0x8000 partition_table/partition-table.bin 0x1000 bootloader/bootloader.bin 0x10000 hello_world.bin
esptool.py v3.0-dev
Serial port /dev/ttyUSB0
Connecting........_
Chip is ESP32D0WDQ6 (revision 0)
Features: WiFi, BT, Dual Core, Coding Scheme None
Crystal is 40MHz
MAC: 24:0a:c4:05:b9:14
Uploading stub...
Running stub...
Stub running...
Changing baud rate to 460800
Changed.
Configuring flash size...
Compressed 3072 bytes to 103...
Writing at 0x00008000... (100 %)
Wrote 3072 bytes (103 compressed) at 0x00008000 in 0.0 seconds (effective 5962.8 kbit/s)...
Hash of data verified.
Compressed 26096 bytes to 15408...
Writing at 0x00001000... (100 %)
Wrote 26096 bytes (15408 compressed) at 0x00001000 in 0.4 seconds (effective 546.7 kbit/s)...
Hash of data verified.
Compressed 147104 bytes to 77364...
Writing at 0x00010000... (20 %)
Writing at 0x00014000... (40 %)
Writing at 0x00018000... (60 %)
Writing at 0x0001c000... (80 %)
Writing at 0x00020000... (100 %)
Wrote 147104 bytes (77364 compressed) at 0x00010000 in 1.9 seconds (effective 615.5 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
Done
```
If there are no issues by the end of the flash process, the board will reboot and start up the `your-project-name` application.

### Monitor the Device
ESP32 can be monitor during working by using this command:
```
idf.py monitor
```
The default serial communication using monitor feature is through UART0. Other UARTs can also be config as another monitoring channels but it will need to be configured by your own config and print functions.
`idf.py monitor` cannot listen to UART1 or UART2, because it's bound to the USB-to-serial used during flashing (UART0 by default).
For ESP-IDF monitor, if IDF monitor fails shortly after the upload, or, if instead of the messages above, you see random garbage similar to what is given below, your board is likely using a 26 MHz crystal. Most development board designs use 40 MHz, so ESP-IDF uses this frequency as a default value.
![image](https://github.com/user-attachments/assets/a34d1bf8-b66b-4e89-ba06-13bfa533c3ac)
If you have such a problem, do the following:
- Exit the monitor
- Go back to `menuconfig`
- Go to `Component config` --> `Hardware Settings` --> `Main XTAL Config` --> `Main XTAL frequency`, then change CONFIG_XTAL_FREQ value to your crystal value.
- After that, `build` and `flash` the application again

For more details on specific `monitor` features, refer to [ESP-IDF Monitor](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/tools/idf-monitor.html)
You can combine building, flashing and monitoring into one step by running:
```
idf.py -p PORT flash monitor --[monitor features]
```

## Common Commands
- `idf.py build`: Compiles the project
- `idf.py flash`: Flashes the compiled binary to ESP32
- `idf.py monitor`: Serial monitor
- `idf.py clean`: Cleans the build directory
- `idf.py size`: Displays binary size info
- `idf.py fullclean`: Cleans all build and configuration data
## Project Structure
```
your_project/
├── build/                  # Generated binaries and build files
├── components/             # Custom components (optional)
├── main/                   # Application source files
│   └── main.c              # Main source files
│   └── CMakeLists.txt      # CMake definition for main application
├── customLibs/             # Library files folder (optional)
│   └── lib1
│       └── lib1.c          # Library 1 Source file
│       └── lib1.h          # Library 1 Header file
│       └── CMakeLists.txt  # CMake definition for library 1 files
|   .
|   .
|   .
│   └── libN
│       └── libN.c          # Library N Source file
│       └── libN.h          # Library N Header file
│       └── CMakeLists.txt  # CMake definition for library 1 files
├── CMakeLists.txt          # Project CMake definition
└── sdkconfig               # Configuration file (after menuconfig)
```
`Libs/` folder is optional can be place anywhere in `your-project`. However, be sure to include this line in Project `CMakeLists.txt`
```
include($ENV{IDF_PATH}/tools/cmake/project.cmake)
set(EXTRA_COMPONENT_DIRS ${CMAKE_CURRENT_LIST_DIR}/{path}/customLibs)
```
## Useful Tips
**Permission Denied Issue**:
With some Linux distributions, you may get the error message similar to `Could not open port <PORT>: Permission denied: '<PORT>'` when flashing the ESP32. This can be solved by adding the current user to the specific group, such as `dialout` or `uucp` group.

**Unsupported Targets**:
Some of examples do not support ESP32 because required hardware is not included in ESP32 so it cannot be supported.
Please check the README file in every example. If this is present including ESP32-type target, or the table does not exist at all, the example will work on ESP32.

**Python Compatibility**:
ESP-IDF supports Python 3.9 or newer. It is recommended to upgrade your operating system to a recent version satisfying this requirement.

**Partition Table**:
ESP-IDF support several type of partition table below:
![image](https://github.com/user-attachments/assets/d20f7825-d09c-49af-8cdd-b8c446b9ea8a)
Custom partition is allowed, using a .csv file with format below:
```
# Name,     Type, SubType, Offset,   Size
nvs,        data, nvs,     0x9000,   24K
otadata,    data, ota,     0xf000,   8K
phy_init,   data, phy,     0x11000,  4K
factory,    app,  factory, 0x10000,  1M
ota_0,      app,  ota_0,   ,         1M
ota_1,      app,  ota_1,   ,         1M
.
.
.
par-name,   app,  par_n,   ,         1M
```
The custom partition can be set by `menuconfig`-->`Partition Table`-->`Partition Table`-->`Custom partition table CSV`. The file path need to be same location with Project `CMakeList.txt`.
The size of number of app partitions depend on the memory flash IC come along with ESP32. Default for ESP32 Dev Board is 4MB.
