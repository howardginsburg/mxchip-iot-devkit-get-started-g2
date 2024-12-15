# Azure IoT DevKit (MXChip AZ3166) Getting Started

The [Azure IoT DevKit (MXChip AZ3166)](https://microsoft.github.io/azure-iot-developer-kit/) board is [discontinued](https://www.seeedstudio.com/AZ3166-IOT-Developer-Kit.html). When first released, it was popular among developers looking to learn IoT.  It's a great board to learn with, and reintroducing a simple experience is the goal of this repo.  Most published samples have been archived as they no longer work with the latest x509 certificate changes in Azure.  The current published [sample](https://learn.microsoft.com/azure/iot/tutorial-devkit-mxchip-az3166-iot-hub) from Microsoft leverages Eclipse ThreadX RTOS connecting to Azure IoT Hub.  ThreadX is great, but there is a learning curve all its own with it.

The original Getting Started project [repo](https://github.com/Azure-Samples/mxchip-iot-devkit-get-started) and [documentation](https://microsoft.github.io/azure-iot-developer-kit/docs/apis/arduino-language-reference/) is the basis of this project.


There are currently several issues with the original project:

1. The IoT Workbench extension for VSCode has been deprecated.
1. The AZ3166 board definition file for Arduino not been updated to the latest IDE requirements, and the IDE experiences an error when trying to process it.
1. Microsoft retired the x509 (Baltimore) certificate that used to be needed to handshake with Azure IoT Hub.  Thus, the sample cannot connect to Azure.

This repo is a duplicate of the initial project, with the following changes:

1. Leverage VSCode and PlatformIO for a robust development experience.
1. Modify the code to support the latest DigiCert G2 certificate required to handshake with Azure IoT Hub.

## Learnings

1. The Azure IoT C SDK is probably where a long term change should be made to support minimal changes for developers.  However, that will involve publishing the overall framework and board definitions.
1. There is a method on the IoT Hub Client SDK that allows you to pass in your own certificate, thus overriding the default.  This is a great way to support the latest certificates without having to wait for the framework to be updated.

## Getting Started

### Prerequisites

1. [Visual Studio Code](https://code.visualstudio.com)
1. [PlatformIO](https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide) extension for VSCode
1. [Azure IoT Hub](https://learn.microsoft.com/azure/iot-hub/create-hub?tabs=portal)
1. [Device](https://learn.microsoft.com/azure/iot-hub/create-connect-device?tabs=portal#add-a-device) defined in IoT Hub with a Symmetric Key
1. [USB driver](https://www.st.com/en/development-tools/stsw-link009.html#get-software) for the AZ3166.

### Setup

1. Clone this repo.
1. Open the project in VSCode.
1. In the PlatformIO extention, select `Upload and Monitor` to build and upload the project to the AZ3166 board.
1. Reset the board into `Access Point` mode by pressing and holding the `B Button` and the `Reset Button`.
1. Connect to the wireless network `AZ-XXXXXXXXXXX` where `XXXXXXXXXXX` is the MAC address of the board.
1. Open a browser to `http://192.168.0.1'.
1. Enter your WiFi SSID and password, and the Azure IoT Hub connection string.
1. The board will reboot and the LCD will display the cycle of connecting to wifi, connecting to Azure IoT Hub, and sending a message to Azure IoT Hub.

## Changes Made from Original Project

1. `GettingStarted.ino` from the original repo is renamed to `main.cpp` to follow PlatformIO conventions.
1. All code changes are in `main.cpp`.  It includes the definition of the G2 certificate, and an addition call to the IoT Hub MQTT Client to pass it in.
1. Search for `G2` to find the changes made in the code
