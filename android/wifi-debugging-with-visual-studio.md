## Android WiFi debugging with Visual Studio
I learned from [this blog](https://www.andrewhoefling.com/Blog/Post/android-wi-fi-debugging-with-adb-android-device-bridge-and-xamarin-visual-studio).

If your device is rooted, there is anothter simple way.

- Make sure your device is connected to your computer.
- USB Debugging is tured on, and the device allows the computer to connect.
- ADB installed correctly on your computer, and the device is regonized. You can use `adb devices` to see the list of connected devices.
- Run the "Android ADB Command prompt..." from Tools -> Android menu in Visual Studio to access to ADB. Excute the following command
```
adb tcpip 5556
```
This command updates the device to listen fro ADB connections on the specified port of 5556.
- Disconnect the device from the computer and make sure it's conntected to the same network over WiFi.
- Using the WiFi settings on the device determine the IP address. For this example, my IP address is 192.168.1.123
- On the computer execute the following command in your ADB command prompt
```
adb connect 192.168.1.123:5556
```
The device will be connected, and you can start debugging.
