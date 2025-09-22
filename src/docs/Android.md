# Android端读写工具 使用文档
 
 - 安卓端需安装两个APK，`spdrw.apk`和`UsbSerialWebSocketServer.apk`

## 下载链接

 - [https://spdrw.cc/Android/spdrw.apk](https://spdrw.cc/Android/spdrw.apk)
 - [https://spdrw.cc/Android/UsbSerialWebSocketServer.apk](https://spdrw.cc/Android/UsbSerialWebSocketServer.apk)

## UsbSerialWebSocketServer.apk 使用文档

将USB串口转换器绑定到WebSocket客户端，基于 [usb-serial-telnet-server](https://github.com/ClusterM/usb-serial-telnet-server) 修改而来。

只需将USB串口适配器连接到Android设备的USB OTG端口，启动此应用程序，然后使用任何WebSocket客户端连接到它，例如：
* 使用同一Android设备上的浏览器（连接到localhost）
* 使用同一网络上的计算机上的WebSocket客户端（通过Wi-Fi连接）
* 使用任何支持WebSocket的客户端应用程序

### 主要特点

✅ **纯文本发送**：客户端发送的文本直接转发到串口  
✅ **纯文本接收**：串口接收的数据直接作为文本发送给客户端  
✅ **无格式转换**：不进行十六进制、Blob等复杂转换  
✅ **简单易用**：就像普通的聊天工具一样简单  
✅ **跨平台兼容**：任何支持WebSocket的客户端都可以使用

### 兼容设备

此应用程序使用 [mik3y的usb-serial-for-android库](https://github.com/mik3y/usb-serial-for-android) 并支持USB转串口转换器芯片：

* FTDI FT232R, FT232H, FT2232H, FT4232H, FT230X, FT231X, FT234XD
* Prolific PL2303
* Silabs CP2102 和所有其他 CP210x
* Qinheng CH340, CH341A, CH340K, CH340X

一些其他设备特定驱动程序：
* GsmModem 设备，例如基于Unisoc的Fibocom GSM调制解调器
* Chrome OS CCD（闭壳调试）

以及实现通用CDC/ACM协议的设备，如：
* Qinheng CH9102
* Microchip MCP2221
* 使用ATmega32U4的Arduino
* 使用V-USB软件USB的Digispark
* ...

### 使用方法

- 安装并启动UsbSerialWebSocketServer应用
- 连接USB串口设备
- 按需是否开启本地连接(Local connections only)
- 记录显示的WebSocket地址（如：`ws://192.168.1.100:8080` 或 `ws://127.0.0.1:8080`）

## spdrw.apk 使用文档

 - 安装并启动spdrw应用
 - 点击顶部的`连接`
 - 输入WebSocket地址（如：`ws://192.168.1.100:8080` 或 `ws://127.0.0.1:8080`）
 - 点击弹窗中的`连接`