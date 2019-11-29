# create-mobile-app-for-polar-sensors
An introduction page for developers to start application design

## General
 
Polar has adopted  wireless Bluetooth Low Energy technology (BLE) in data communication between Sensors, Training Computers and Mobile applications.
BLE is suitable for IoT ecosystems where interoperability and seamless data streams across various interfaces and devices are key qualifiers.
 
Bluetooth SIG has defined many GATT based Profiles and Services that are optimized for low data rates and power consumption. Technology is constantly evolving and latest releases of these specifications are available at https://www.bluetooth.com/specifications/gatt/
 
 
 ## Getting Started
 
For creating an application that communicates with Polar sensor doesn't require contract with Polar as sensor implementation follows Bluetooth standards.
However, some sensor models are capable to deliver data over BLE that are excluded from standard profiles and services, such as ECG or acceleration signals.
Access to proprietary content of Polar sensor data is available via Polar BLE SDK in GIT Hub https://github.com/polarofficial/polar-ble-sdk. Also, SDK provides simple API for connecting with Polar HR sensors and reduces design workload in contrast to creating BLE connection related code from scratch.   
 
On multiple websites and Blogs a Developer may find useful information on required tools, API’s, development environments and code examples to start development of own Application.
https://www.bluetooth.com/blog/part-2-the-wheels-on-the-bike-are-bluetooth-smart-bluetooth-smart-bluetooth-smart/
https://developer.android.com/guide/topics/connectivity/bluetooth-le.html
https://code.msdn.microsoft.com/windowsapps/Bluetooth-Generic-5a99ef95
https://developer.apple.com/bluetooth/
 
Developing Bluetooth application needs information on sensor capabilities. A full list of supported features and Bluetooth Characteristics by Polar sensors are available on Bluetooth SIG webpage.
Use sensor name to find Declaration ID that exposes supported protocol layers. To get an idea of starting development and potential content for application, here's a brief description of H10 Sensor operation logic and supported Services.
 
 ### H10
Once Sensor (electrode areas on the reverse side) detects skin contact, Bluetooth Low Energy starts in Peripheral role (as a Sensor) and advertises to be connectable with a Collector (phone or wrist unit). When the Collector sends a Connection Request after a detected advertising message, the Sensor accepts it and a short pairing phase will start if needed. After pairing is finished, the Collector is supposed to enable heart rate notifications from the Sensor by writing value 0x01 to the Client Characteristic Configuration descriptor.
Sensor is measuring heart rate value once in a second and sends HR value (uint8) as a Heart Rate Measurement Notification. In addition, Polar H10 Sensor support RR Intervals (unit of 1/1024 seconds), but not energy expenditure value in Heart Rate Characteristic. In case of the skin contact is absent for 20-30 seconds, the Sensor will start termination of BLE connection and switches back to standby mode to save power.
 
 ### Supported services
- Heart Rate Service (HRS) for providing heart rate measurement results
- Battery Service (BAS) for providing battery status information. H10 supports indication for changed battery status
- Device Information Service (DIS) for providing information from sensor
- User Data Service (UDS) for exposing user-related data in the sports and fitness environment
 
 ### Other Polar sensors
Polar product portfolio includes alternative BLE solutions for monitoring Athlete's progress, such as optical heart rate (OH1), Stride, Biking Power/Speed/Cadence sensors.
Application development is similar process as described above for H10, even though the delivered content is sensors specific. For example, OH1 is measuring user's heart rate optically, and hence it can't support RR intervals. Complete set of supported services are  available in Bluetooth SIG's web page.
 
 ### Happy Coding Sessions!
