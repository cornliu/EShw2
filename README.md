# Embedding System HW2

### Tool used
* matplotlib
* socket
* mbed

### How to use

#### At first, please change some wifi setting to yours.   
  * change "./mbed_app.json"  line 14-15
    ```
      "nsapi.default-wifi-ssid": "\"YourWIFIname\"",
      "nsapi.default-wifi-password": "\"Password\"",
    ```
    for example,
    ```
      "nsapi.default-wifi-ssid": "\"myphone\"",
      "nsapi.default-wifi-password": "\"abcdefg\"",
    ```
    
    !!! ATTENTION
    * If your wifi name includes characters not in english, it may have problem while connecting
    * Please do not take off   ```\"```, it is important for maintaining string type.
 
  * change "./ws_server.py" line 13, line 25-26
    ```
    # line 1
      mode = 2  # can switch between 1 and 2 to test
    # line 25 - 26
      HOST = 'xxx.xxx.xxx.xxx' # change to the IPv4 address of your computer
      PORT = 62023 # change to any number you like from 49152-65535
    ```
    
  * change "./source/main.cpp" line 51, line 119
    ```
    // line 51
      static constexpr size_t REMOTE_PORT = 62023; // standard HTTP port // change to the same number as the one in "./ws_server.py"
    // line 119
      address.set_ip_address("xxx.xxx.xxx.xxx"); // change to the HOST address as the one in "./ws_server.py"
    ```
    
#### Start the server
  ```
  python3 ws_server.py
  ```
  
#### Run mbed
Press "Run Program" button
  
 
##### !!! ATTENTION
* The server should be started before the mbed program runs. Or there may be the error
  ```
  OSError: [Errno 48] Address already in use
  ```
  Then you should change a new port number, or restart both mbed and server.
* If you choose the port number out of range, the error may occur
  ```
  OverflowError: getsockaddrarg: port must be 0-65535.
  ```

### Expected output

(Assuming you are using a wifi interface, otherwise the scanning will be skipped)

```
Starting socket demo

2 networks available:
Network: Virgin Media secured: Unknown BSSID: 2A:35:D1:ba:c7:41 RSSI: -79 Ch: 6
Network: VM4392164 secured: WPA2 BSSID: 18:35:D1:ba:c7:41 RSSI: -79 Ch: 6

Connecting to the network...
IP address: 192.168.0.27
Netmask: 255.255.255.0
Gateway: 192.168.0.1

Resolve hostname ifconfig.io
ifconfig.io address is 104.24.122.146

sent 52 bytes: 
GET / HTTP/1.1
Host: ifconfig.io
Connection: close

received 256 bytes:
HTTP/1.1 200 OK

Demo concluded successfully 
```
