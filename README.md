# SuperSU Installer
这是一个在基于 Unisoc/Spreadtrum SP9820E SoC 的智能手表上获取root权限的软件。该方法应该能适用于所有型号的手表，例如 A36E, Wonlex KT11, Lemfo G4H 4G等（我不认识）。该程序利用了制造商的后门而实现

这个仓库的README为小天才手表优化，适用手表为Z1y/s, Q1y/s等采用了SP9820E SoC的手表

## 食用方法

### 启用ADB调试

对于小天才手表来说，只需要在拨号盘输入 `*#0769651#*` 即可

### 安装SuperSU Installer
1. [下载](https://github.com/ZH-XiJun/SuperSUInstaller/releases/) 或自行编译SupersuInstaller
2. 安装 小天才启动器 到手表，位置同上下载链接，安装方法同下
3. 下载 SuperSU_ForXTC.apk 到电脑（无需安装），位置同上下载链接
4. 安装此app到手表
```
C:\Users\Administrator>adb push SuperSUInstaller.apk /sdcard/1.apk # 将apk上传至手表
C:\Users\Administrator>adb shell                                   # 进入安卓shell环境
shell@sp9820e_xtc:/ $ pm install /sdcard/1.apk                     # 使用pm安装软件
        pkg: /sdcard/1.apk
Success
```
`adb shell` 与 `pm install` 一定要分开执行，否则会被pm锁拦截！
D3等较新机型在执行adb push指令时时可能会遇到 `adb push is not allowed by XTC` ，这时候请[解除Push锁](https://github.com/ReX-iMoo-Team/iMoo-Toolkit)后再试

### 刷入 SuperSU
1. 在手表设置中关闭WiFi
2. 打开拨号盘，输入 `*#*#83781#*#*`
3. 在弹出的页面中切换到 CONNECTIVITY 界面
4. 点击 "Start Service"
5. 点击 "Wifi eut" 并在弹出的窗口中点 "OK"
6. 在电脑上执行这条指令以启动Supersu Installer：
```
adb shell 'am start -n ru.eisaev.supersuinstaller/.MainActivity'
```
7. 等待APP显示 "Hello World!"
8. 将你下载到的 SuperSU_ForXTC.apk 安装至手表，方法同上 [“安装SuperSU Installer”](https://github.com/ZH-XiJun/SuperSUInstaller#%E5%AE%89%E8%A3%85supersu-installer)
10. 使用 小天才启动器 启动SuperSU软件，提示更新SU二进制，点 “常规方式”，升级成功后重启手表
11. 重启完毕后再次启动SuperSU，检查root状态
14. 在 设置-默认操作 中将询问改成授权，否则SuperSU不弹窗，无法授权root！

现在你可以在手表上随意使用root，在adb上也是一样：
```
C:\Users\Administrator>adb shell
shell@sp9820e_xtc:/ $ su
root@sp9820e_xtc:/ # id
uid=0(root) gid=0(root) context=kernel
```
图文教程可看[B站专栏](https://www.bilibili.com/read/cv20433593?spm_id_from=333.999.0.0)，原作者[eisaev](https://github.com/eisaev)，原项目地址[点此](https://github.com/eisaev/SuperSUInstaller/)
