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
5. [Compiling and Flashing](#compiling-and-flashing)
6. [Common Commands](#common-commands)
7. [Project Structure](#project-structure)
8. [Useful Tips](#useful-tips)

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

7. ESP-IDF Tools Installer also creates a shortcut in the Start menu and Desktop for these 2 options to launch the ESP-IDF. These shortcuts launch the corresponding environment and runs `export.bat` script to set up the environment variables (`PATH`, `IDF_PATH` and others). Inside theses, all the installed tools are available.
8. These shortcuts are specific to the ESP-IDF directory selected in the ESP-IDF Tools Installer. If you have multiple ESP-IDF directories on the computer (for example, to work with different versions of ESP-IDF), you have two options to use them:
   - Create a copy of the shortcut created by the ESP-IDF Tools Installer, and change the working directory of the new shortcut to the ESP-IDF directory you wish to use.
   - Alternatively, run `cmd.exe` or `powershell.exe`, then change to the ESP-IDF directory you wish to use, and run `export.bat`. Note that unlike the previous option, this way requires `Python` and `Git` to be present in `PATH`. If you get errors related to                `Python` or `Git` not being found, use the first option.
### Linux
These are the steps for setting up the ESP-IDF for your ESP32.
- Install Prerequisites
- Get ESP-IDF

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
### MacOS
These are the steps for setting up the ESP-IDF for your ESP32.
- Install Prerequisites
- Get ESP-IDF

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
  
For more details and error resolve, consult [ESP-IDF Setup for MacOS](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html#get-started-get-esp-idf).
## Environment Setup

## Creating a New Project

## Compiling and Flashing

## Common Commands

## Project Structure

## Useful Tips
