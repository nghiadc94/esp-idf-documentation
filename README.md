# Espressif ESP-IDF Documentation

This document provides a step-by-step guide to set up and use the Espressif IoT Development Framework (ESP-IDF) for developing firmware on ESP32 microcontrollers.

## Table of Contents
1. [Requirement](#requirements)
2. [Installation](#installation)
    - [Windows](#windows)
    - [Linux](#linux)
    - [macOS](#macos)
3. Environment Setup
4. Creating a New Project
5. Compiling and Flashing
6. Common Commands
7. Project Structure
8. Useful Tips

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
        - Alternatively, run `cmd.exe` or `powershell.exe`, then change to the ESP-IDF directory you wish to use, and run `export.bat`. Note that unlike the previous option, this way requires `Python` and `Git` to be present in `PATH`. If you get errors related to `Python` or `Git` not being found, use the first option.
