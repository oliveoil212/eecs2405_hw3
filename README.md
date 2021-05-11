# hw3

## Set up 
Except for main.cpp, config.h, wifi_mqtt/mqtt_client.py, mbed_app.json and magic_wand_model_data.cpp, other files are identical to  labs.You can simply copy  libraries from your lab and replace those files and skip the following steps

1. Add "4DGL-uLCD-SE" library to the current project 
```shell=
 git clone https://gitlab.larc-nthu.net/ee2405_2021/4dgl-ulcd-se.git
 rm -rf ./4dgl-ulcd-se/.git
```
2. Import RPC Library
```shell=
$ mbed add https://gitlab.larc-nthu.net/ee2405_2021/mbed_rpc.git
```
3. Import BSP library for running accelerometer.
```shell= 
mbed add http://developer.mbed.org/teams/ST/code/BSP_B-L475E-IOT01/#bfe8272ced90
```
4. Import tensorflow
```shell= 
mbed add https://gitlab.larc-nthu.net/ee2405_2021/tensorflowlite_mbed
```
5. Import Mqtt Library
```shell=
 mbed add https://gitlab.larc-nthu.net/ee2405_2019/wifi_mqtt.git
```
6. Revise the host ip and wifi configuration. see lab10
7. Then, please remove ./wifimqtt/main.cpp 
8. Skip the steps below, if no error occurs. :laughing: 
9. Make sure pyserial was installed, if not  see lab9.4.3
10. Add ISM43362 library into mbed-os.
```shell=
mbed add wifi-ism43362
```
9. Set up mqtt. see lab10.4.4

## How to run
1. compile the program
```shell=
sudo mbed compile --source . --source ~/ee2405/mbed-os-build/ -m B_L4S5I_IOT01A -t GCC_ARM --profile tflite.json -f
```
2. execute python client
```shell=
sudo python3 wifi_mqtt/mqtt_client.py
```
3. Acesses the serail port
```shell=
sudo screen /dev/ttyACM0
```
### RPC function


| RPC Command | Function                  |
| ----------- | ------------------------- |
| /mode/run 0 | gesture UI mode           |
| /UI/run     | gesture UI mode           |
| /mode/run 1 | tilt angle detection mode |
| /detect/run | tilt angle detection mode |
### Gesture
The "you cant see me" gesture of John Cena
### Threshold angle
Default value: **30°** degrees.  

options: 30°、40°、50°、60° 
## The result
ulcd  

![](https://i.imgur.com/LTXpdSw.jpg)


![](https://i.imgur.com/ZkqVhUT.png)

### UI mode
If you send  **"/mode/run 0"** or **/UI/run** to mbed, the blue led turns  on and mbed would response **"gesture UI mode"**.
<!-- Using the gesture to select the threshold angle on uLCD. -->
After pushing  the user buttom, you will see this result on mqtt_client.py
<!-- ![](https://i.imgur.com/NKO6XBi.png) -->
![](https://i.imgur.com/jqsUVJD.png)



### Tilt angle detection mode
If you send  **"/mode/run 1"** or **/detect/run** to mbed, the orange led turns  on and mbed would response **"tilt angle detection mode\n"**.



| ![](https://i.imgur.com/drSVMEv.png) | ![](https://i.imgur.com/rdDWTz4.png) |
| -------- | -------- |

<!-- ![](https://i.imgur.com/Rgxc5Gu.png) -->

Green Led would blink. As it is blinking, please place mbed  on  table, then mbed would  assume this is the stationary position.



After 10 message arrived, this mode would be terminated and mbed will respone **"back to RPC mode\n"**
![](https://i.imgur.com/u0CfntG.png)
