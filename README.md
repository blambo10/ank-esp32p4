## ESP32P4 Dev Board Sync Project using ESP-IDF

This project is designed to sync data from one esp32p4 controller to another over the UART protocol.It contains two source files a main.c which is intended for primary controller and slave.c intended for the board that is to receive the data from the primary [main.c](main/main.c). The file is located in folder [main](main).

 The project build configuration is contained in `CMakeLists.txt` it has been updated to look for environment variables which will determine if the build will execute using either master.c or slave.c respectively

Below is short explanation of remaining files in the project folder.

```
├── CMakeLists.txt
├── pytest_hello_world.py      Python script used for automated testing
├── main
│   ├── CMakeLists.txt
│   └── main.c
│   └── slave.c
└── README.md                  This is the file you are currently reading
```

## Connecting to respective board on comm port

* run `idf.py -p PORT monitor`

## Build master.c 

* idf.py build -DCONFIG_NAME=slave_config

## Build slave.c 

* idf.py build -DCONFIG_NAME=master_config

## deploy to board & monitor

After running above for the respective board ensure you have the COM port corresponding to the appropriate board and run the following 

* idf.py -p COM3 clean flash monitor


### Current Progress on bluetooth

The ESP32P4 integrated dev board being used contains a slave controller esp32c6 which is used to perform the wireless comms including bluetooth, to enable this chip using esp-idf you must update the sdkconfig.

The following need to be configured

```
#
# ESP32-C6 is Slave Target from Wi-Fi Remote Component
#
CONFIG_ESP_HOSTED_P4_DEV_BOARD_NONE=y
# CONFIG_ESP_HOSTED_P4_DEV_BOARD_FUNC_BOARD is not set
CONFIG_ESP_HOSTED_PRIV_SDIO_OPTION=y
CONFIG_ESP_HOSTED_PRIV_SPI_HD_OPTION=y
# CONFIG_ESP_HOSTED_SPI_HOST_INTERFACE is not set
CONFIG_ESP_HOSTED_SDIO_HOST_INTERFACE=y
# CONFIG_ESP_HOSTED_SPI_HD_HOST_INTERFACE is not set
# CONFIG_ESP_HOSTED_UART_HOST_INTERFACE is not set
CONFIG_ESP_HOSTED_IDF_SLAVE_TARGET="esp32c6"
```