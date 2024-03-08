# 中兴远航30s小白向解锁BL+解锁Root流程

一周前刚从🐟上购入6+128的全新远航30s（套娃机，名字还叫vikk v16 plus），非常感谢大佬！让我立刻就能root远航30s。大佬的解锁教程位于github链接，但我作为菜狗中间还是踩了不少坑，所以打算补充完善一下大佬的教程，以小白向的流程发布（这或许也是中兴系第一个展锐处理器小白解锁教程hhhh）

## 前提条件
- 请确保手机电量充足！！至少在80%以上供你折腾！
- 学会并可以执行adb命令，如果不会的话去百度吧。
- 学会并可以执行cmd命令，你最好已经学会在windows终端中执行cmd命令。

## BL解锁步骤
1. 下载并解压windows端展锐驱动 https://androiddatahost.com/dsa6h ，找到你的系统对应版本文件夹，然后找到DriverSetup.exe以及DPInst64.exe安装（linux端及驱动安装失败的，请参考大佬的github链接）
2. 下载解锁脚本，我上传了蓝奏云蓝奏云链接 https://wwi.lanzoup.com/iQJx01qpioni 。关闭杀毒软件然后解压
3. 手机关机，数据线连接电脑
4. 找到unlock_emmc.bat，使用管理员权限打开，其会等待30s
5. 长按手机音量减，手机会进入下载模式（电脑应该会听到有设备连接的声音），此时手机黑屏是正常情况
6. 脚本会自动运行，根据脚本提示运行脚本，脚本会运行多次。如果是等待10s就等待；如果显示pause，当你听到手机再次连接电脑之后，回车跳过pause【请抓紧时间，不要让手机脱离黑屏状态】。
7. 脚本会自动备份boota.img/bootb.img，该过程非常缓慢，耐心等待（emmc是这样的）
8. 解锁完成之后手机会进入一个蓝白色界面（fastbootd界面），请手动进入recovery模式，并且清除数据，recovery界面如下图所示
9. 清除完成数据即可开机，此时手机左上角显示如下小字，即为bl解锁成功。
10. 第一次开机时间较长（卡在myos界面），请耐心等待。如果15min后仍卡第二屏（myos），重刷系统完整包（见附录）

### 解BL常见问题
1. 解锁完成之后卡第一屏（厂商logo）并且无限重启
   - 说明没有清除数据，建议重刷系统完整包（见附录）
2. 脚本提示无法写入
   - 如果是无法写入uboot，可以在脚本最后将特定代码修改为特定的erase和write指令组合，以确保可以写入。
3. 脚本卡在读取boot.img
   - emmc是这样的，时间很长。如果等不了，或者你是11系统无需备份boot的话，可以删除读取boot部分。
4. 解锁完成之后卡第二屏（MyOS）
   - 进fastbootd重刷系统完整包（见附录）

## Root解锁步骤
1. 首先确保你的手机系统为最新的11.5.11系统（MyOS11.5.11_7531N_UNI_H），如果不是的话（例如vikk系统，例如06系统，03系统），请重刷系统完整包（见附录）并ota更新至11系统
2. 下载大佬制作好的远航30s，11系统版本boot（boot已经修补magisk并签名）。下载链接：[https://wwi.lanzoup.com/inhZc1qps6ah](https://wwi.lanzoup.com/inhZc1qps6ah)
3. 进入fastbootd模式（蓝白界面），使用fastboot enhance刷写boot2309-27000.img，你是a槽位的系统就刷boot_a分区，你是b槽位的系统就刷boot_b分区。
4. 如果你是ota到11版本的系统，它会提示存在system_a/b_cow分区，是否强行刷入，强行刷入boot分区即可。
5. 清除数据并重启手机，第一次开机时间较长，请耐心等待。
6. 开机完成后下载magisk27版本，下载链接[https://mrzzoxo.lanzoui.com/ivf891nh5zsf](https://mrzzoxo.lanzoui.com/ivf891nh5zsf)，打开后提示修复magisk环境，等他自动修复并重启即可。
7. 可以通过adb shell命令进入shell，输入su测试是否root成功。

### 刷Root常见问题
1. 我的系统版本不是11.5.11，且无法ota升级到该版本
   - 如果是版本号大于11的（5g+4g版本），请自行修补boot并签名（详见大佬github），这需要一定计算机基础。
   - 如果版本号小于11，请刷系统完整包（参照附录）
2. 刷完boot之后卡第一屏
   - 如果你是手动修补的boot，请根据大佬的github进行正确的签名，然后重新刷入签名后的boot。
   - 如果还是不行/其他情况，请刷系统完整包（见附录），确保能开机后再重新刷入boot
3. 刷root卡第二屏（MyOS）超过15min
   - system分区损坏，重刷系统完整包

## 附录
### 附录1：如何进入fastbootd模式？
- 首先下载fastboot enhance，github链接 https://github.com/libxzr/FastbootEnhance/releases ，下载里面的release.zip，打开界面如图
- 如果你是开机状态，那么执行adb reboot fastboot，然后fastboot enhance将可以看到该设备，双击后重启到fastbootd模式。如果你无法正常开机，那么再次执行大佬的bat脚本unlock_emmc.bat，执行结束后将会自动进入fastbootd模式

### 附录2：如何刷系统完整包（官网11.5.06系统）
1. 下载官网11.5.06版本的包（如果你的版本号大于11，说明你是5g+4g版本，你需要自己修补boot⚠）下载链接：https://www.ztedevices.com/cn/supports/%e8%bf%9c%e8%88%aa30s/
2. 下载完成之后解压第一层，得到update.zip,放置待用
3. 再解压一层，得到payload.bin，放置待用。
4. 进入fastbootd模式（见附录1），刷写payload.bin，选择解压出来的payload.bin并刷入
5. 从fastbootd模式进入recovery模式，高级选项里选择adb更新系统，然后执行 adb sideload D:\\update.zip （这里写你放置update.zip的位置）
6. 手机会自动升级，如果升级到94%显示升级失败，是正常情况（是个无关紧要的error），忽略即可。
7. 清除用户数据，重启应该就可以开机了，第一次开机时间较长属于正常情况。

#### 附录2中的常见问题
- recovery进行sideload升级时，升级到47%报错
  - 这是因为recovery不允许降级，可以通过在fastbootd中强刷boot解决。重新进入fastbootd模式，在fastboot enhance中提取payload.bin里的boot.img（下图界面找到boot并导出镜像），用提取的官方boot.img刷写你系统槽位所在分区(boot_a/boot_b)。
- recovery进行sideload升级时，出现其他报错
  - 找到并进入recovery升级日志，翻到 倒数几页，去看看哪里error了。这里仅提供一个问题的解决方法，其他问题请自行根据日志解决

### 修补boot中的一个细节【多机型通用tip】
如何获得镜像的fingerprint以及osversion？
在大佬的教程第四步中，你需要提供如下的正确信息
- $FINGERPRINT
- $OS_VERSION
你可以使用 ./avbtool info_image --image vbmeta.img 命令来获取相关的信息，如果vbmeta.img中没有相关信息，可以在vbmeta_system.img中获取

仅供学习参考，如果有不对的地方，还请各位大佬多多指教！

（中兴远航41，畅行50与小鲜50原理上也可以解锁bl，有兴趣的大佬可以自主参考 https://github.com/TomKing062/CVE-2022-38694_unlock_bootloader/wiki/AddSupportToModel 进行尝试）
（另：大佬的工具已经支持解锁大量展锐设备bl，有兴趣的朋友可以去大佬的github看看点个star）
