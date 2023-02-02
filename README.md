# SuperSU Installer
这是一个在基于 Unisoc/Spreadtrum SP9820E SoC 的智能手表上获取root权限的软件。该方法应该能适用于所有型号的手表，例如 A36E, Wonlex KT11, Lemfo G4H 4G等（我不认识）。该程序利用了制造商的后门而实现

这个仓库专为小天才手表适配，适用手表为Z1y/s, Q1y/s等采用了SP9820E SoC的手表

## 食用方法

### 启用ADB调试

对于小天才手表来说，只需要在拨号盘输入 `*#0769651#*` 即可

### 安装SuperSU Installer
1. [下载](https://github.com/ZH-XiJun/SuperSUInstaller/releases/) 或自行编译SupersuInstaller
2. 安装 小天才启动器 到手表，位置同上下载链接
3. 安装此app到手表
```
adb push SuperSUInstaller.apk /sdcard/1.apk
```
### Installing SuperSU
1. Disable WiFi (Settings->Wifi).
2. Open the dialer (Phone).
3. Enter `*#*#83781#*#*` (you do not need to press the green button).
4. In the engineering menu that opens, switch to the "CONNECTIVITY" tab.
5. Click "Start Service"
6. Select "Wifi eut" and click "OK"
7. Run the SuperSUInstaller using adb:
```
adb shell 'am start -n ru.eisaev.supersuinstaller/.MainActivity'
```
8. Wait for the message "Hello World!" to appear.
9. Open File Explorer (Settings->Clear tools->File Explorer) and find SuperSU-v2.82-SR5.apk file (Local).
10. Install SuperSU-v2.82-SR5.apk and run it immediately after installation by clicking "Open".
11. Confirm the binary update using the "Normal" mode.
12. After the update is complete, confirm that the device is rebooted.
13. After booting the device, run the SuperSU GUI again:
```
adb shell 'am start -n eu.chainfire.supersu/.MainActivity'
```
14. Select "SETTINGS" tab and switch "Default access" to "Grant" (unfortunately, the prompt does not appear on these devices).

Now you can use applications that require root permissions, as well as use the root console using adb:
```
$ adb shell
shell@G4E:/ $ su
root@G4E:/ # id
uid=0(root) gid=0(root) context=kernel
```

