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
