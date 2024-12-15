# Azure IoT DevKit (MXChip AZ3166) Getting Started

The [Azure IoT DevKit (MXChip AZ3166)](https://microsoft.github.io/azure-iot-developer-kit/) board is [discontinued](https://www.seeedstudio.com/AZ3166-IOT-Developer-Kit.html).  It's a great board to learn with, and a simple experience is the goal of this repo.  When it was originally released, a VSCode extension was available to help you get started with an Arduino development experience.  That extension is no longer available, and the last published [sample](https://learn.microsoft.com/azure/iot/tutorial-devkit-mxchip-az3166-iot-hub) leverages Eclipse ThreadX RTOS connecting to Azure IoTHub.  All other samples have been retired/archived.

The original Getting Started Arduino project [repo](https://github.com/Azure-Samples/mxchip-iot-devkit-get-started) is the basis of this project.  There are currently several issues with the original project.

1. As the Ardunio IDE has evolved, the board definition file for the AZ3166 has not been updated to the latest IDE requirements, and the IDE experiences an error when trying to process it.
1. Microsoft retired the x509 certificate that used to be needed to handshake with Azure IoTHub.  Thus, the sample cannot connect to Azure.

This repo is a duplicate of the initial project, with the following changes:

1. It has been converted to a PlatformIO project for a robust development experience.
1. A few extra lines of code have been added to support the latest DigiCert G2 certificated required to handshake with Azure IoTHub.

## Getting Started

### Prerequisites

1. Visual Studio Code.
1. PlatformIO extension deployed to VSCode.
1. Azure IoT Hub deployed
1. Device created in Azure IoT Hub

### Setup

1. Clone this repo.
1. Open the project in VSCode.
1. In the PlatformIO extention, select `Upload and Monitor` to build and upload the project to the AZ3166 board.
1. Reset the board into `Access Point` mode by pressing and holding the `B Button` and the `Reset Button`.
1. Connect to the wireless network `AZ-XXXXXXXXXXX` where `XXXXXXXXXXX` is the MAC address of the board.
1. Open a browser to `http://192.168.0.1'.
1. Enter your WiFi SSID and password, and the Azure IoTHub connection string.
1. The board will reboot and the LCD will display the cycle of connecting to wifi, connecting to Azure IoTHub, and sending a message to Azure IoTHub.

## Changes Made

1. `GettingStarted.ino` from the original repo is renamed to `main.cpp` to follow PlatformIO conventions.
1. All code changes are in `main.cpp`.  It includes the definition of the G2 certificate, and an addition call to the IoTHub MQTT Client to pass it in.
1. Search for `G2` to find the changes made in the code
