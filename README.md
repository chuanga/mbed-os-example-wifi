# mbed-os-example-wifi #

Wi-Fi example for Mbed OS

## Getting started with the Wi-Fi API ##

This is an example of a Wi-Fi application using the Wi-Fi and network socket APIs that [Mbed OS](https://github.com/ARMmbed/mbed-os) provides.

The program brings up the Wi-Fi and the underlying network interface and uses it to scan available networks, connects to a network, prints interface and connection details and performs an HTTP operation.

For more information about Wi-Fi APIs, please visit the [Mbed OS Wi-Fi](https://os.mbed.com/docs/latest/reference/wi-fi.html) documentation.

### Supported hardware ###

* [Advanteh WISE-1530 module](https://os.mbed.com/modules/advantech-wise-1530/) built-in Wi-Fi module.
  *(The Mbed target board the Wi-Fi shield connects to shouldn't have any other network interface, for example Ethernet.)*

This example has been modified to use easy-connect library. 

##  Getting started ##

1. Import the example.

   ```
   git clone https://github.com/chuanga/mbed-os-example-wifi
   cd mbed-os-example-wifi
   ```
   
2. Configure the Wi-Fi shield to use.

   Edit ```mbed_app.json``` to include SSID and password:

   ``` 
       "config": {
           "network-interface": {
               "help": "Options are ETHERNET, WIFI_ESP8266, WIFI_WICED",
               "value": "WIFI_WICED"
           },
           "wifi-ssid": {
               "help": "WiFi SSID",
               "value": "\"SSID\""
           },
           "wifi-password": {
               "help": "WiFi Password",
               "value": "\"Password\""
           }
       },
   ```
   
   For built-in Wi-Fi, ignore the value of `wifi-shield`.
   
   The target override configuration for MTB_ADV_WISE_1530 has been provided.
   The configuration assumes that you are using WISE-ED22 module to provide Dap-link connection.
   If you are using MTB board, simply remove the target.stdio_uart_tx/studio_uart_rx options in target_overrides section.

3. Compile and generate binary.

   For example, for `GCC`:

   ```
   mbed compile -t GCC_ARM -m MTB_ADV_WISE_1530
   ```
   
 4. Open a serial console session with the target platform using the following parameters:
 
    * **Baud rate:** 115200
    * **Data bits:** 8
    * **Stop bits:** 1
    * **Parity:** None
 
 5. Copy or drag the application `mbed-os-example-wifi.bin` in the folder `mbed-os-example-wifi/BUILD/<TARGET NAME>/<PLATFORM NAME>` onto the target board.
 
 6. The serial console should display a similar output to below, indicating a successful Wi-Fi connection:
 
 ```
 WiFi example

Scan:
Network: Dave Hot Spot secured: Unknown BSSID: 00:01:02:03:04:05 RSSI: -58 Ch: 1
1 network available.

Connecting...
Success

MAC: 00:01:02:03:04:05
IP: 192.168.0.5
Netmask: 255.255.255.0
Gateway: 192.168.0.1
RSSI: -27

Sending HTTP request to www.arm.com...
sent 38 [GET / HTTP/1.1]
recv 64 [HTTP/1.1 301 Moved Permanently]

Done
```

## Troubleshooting

If you have problems, you can review the [documentation](https://os.mbed.com/docs/latest/tutorials/debugging.html) for suggestions on what could be wrong and how to fix it.
