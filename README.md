# SuperSU Installer
这是一个在基于 Unisoc/Spreadtrum SP9820E SoC 的智能设备上获取root权限的软件。该方法应该能适用于所有使用该方案的设备，例如 小天才手表（Z1/Q1/D3）、360手表（如9X、P2）、米兔手表（如3c、4x）等。该程序利用了制造商的后门而实现

## 食用方法

### 启用ADB调试

对于小天才手表来说，只需要在拨号盘输入 `*#0769651#*` 即可

对于米兔手表来说，在设置中按住`二维码`或`手表空间`（如无二维码）并上下滑动，随后按住`关于`，在接下来的界面中输入`DkTs69`进入售后测试页面，找到原生设置后进入关于页面连续按版本号7下，然后返回找到开发者选项并打开USB调试即可

对于360手表来说，打开设置并按住标题即可进入密码输入界面。该密码随不同设备而变动，有专门的计算工具计算密码。请寻找相关人员获取帮助。获得密码后，进入调试菜单，打开ADB调试即可。

### 安装SuperSU Installer
1. [下载](https://github.com/ZH-XiJun/SuperSUInstaller/releases/) 或自行编译SupersuInstaller
2. 对于小天才来说，安装`小天才启动器`到手表，位置同上下载链接，安装方法同下
3. 下载 SuperSU_ForXTC.apk 到电脑（无需安装），位置同上下载链接
4. 安装此app到手表
```
C:\Users\Administrator>adb push SuperSUInstaller.apk /sdcard/1.apk # 将apk上传至手表
C:\Users\Administrator>adb shell                                   # 进入安卓shell环境
shell@sp9820e_xtc:/ $ pm install /sdcard/1.apk                     # 使用pm安装软件
        pkg: /sdcard/1.apk
Success
```
对于小天才来说，`adb shell` 与 `pm install` 一定要分开执行，否则会被pm锁拦截！

对于360、米兔来说，直接使用指令`adb install`即可

D3等较新机型在执行adb push指令时时可能会遇到 `adb push is not allowed by XTC` ，这时候请[解除Push锁](https://github.com/ReX-iMoo-Team/iMoo-Toolkit)后再试

### 刷入 SuperSU

**你可能需要先调整dpi后再执行下面操作，指令为`adb shell wm density 120`，这会将dpi调整为120，事后使用`adb shell wm density reset`即可恢复**

1. 在手表设置中关闭WiFi
2. 打开拨号盘，输入 `*#*#83781#*#*`，或使用adb指令`adb shell am start com.sprd.engineermode/com.sprd.engineermode.EngineerModeActivity`
3. 在弹出的页面中切换到 CONNECTIVITY 界面
4. 点击 "Start Service"
5. 点击 "Wifi eut" 并在弹出的窗口中点 "OK"

**此步骤后不可退出该界面，直到第6步指令执行成功**

6. 在电脑上执行这条指令以启动Supersu Installer：
```
adb shell am start -n ru.eisaev.supersuinstaller/.MainActivity
```
7. 等待APP显示 "Hello World!"
8. 将你下载到的 SuperSU_ForXTC.apk 安装至手表，方法同上 [“安装SuperSU Installer”](https://github.com/ZH-XiJun/SuperSUInstaller#%E5%AE%89%E8%A3%85supersu-installer)

   对于小天才来说，使用 小天才启动器 启动SuperSU软件

   对于米兔与360来说，请在各自的[调试菜单](#启用adb调试)中找到`三方应用`选项，然后找到SuperSU的包名`eu.chainfire.supersu`并点入
9. SuperSU应提示提示更新SU二进制，点 “常规方式”，更新成功后重启手表
10. 重启完毕后再次启动SuperSU，检查root状态
11. 在 设置-默认操作 中将询问改成授权，否则SuperSU不弹窗，无法授权root！

现在你可以在手表上随意使用root，在adb上也是一样：
```
C:\Users\Administrator>adb shell
shell@sp9820e_xtc:/ $ su
root@sp9820e_xtc:/ # id
uid=0(root) gid=0(root) context=kernel
```
图文教程可看[B站专栏](https://www.bilibili.com/read/cv20433593?spm_id_from=333.999.0.0)，原作者[eisaev](https://github.com/eisaev)，原项目地址[点此](https://github.com/eisaev/SuperSUInstaller/)
