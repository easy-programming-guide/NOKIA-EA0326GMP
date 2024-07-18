# NOKIA EA0326GMP + OpenClash 教程


> 声明：本仓库仅用于个人学习研究，请勿将资料用于商业用途。


## 前置准备

- 准备一台电脑，并安装好 `git`
- 把本仓库克隆到本地，`git clone https://github.com/easy-programming-guide/NOKIA-EA0326GMP.git`
- 一根网线
- 一台 NOKIA EA0326GMP 路由器
- NOKIA EA0326GMP 已经刷好 uboot 固件，并且已经安装好 `ssh` 服务，关于这一步请移步恩山论坛或者其他大神，这里就不再赘述了。


## 本教程提供的和步骤最后一次验证的日期是 2024-07-18 


## 教程步骤


### 第一步：刷入固件，修改默认 LAN 口 IP

1. 使用 uboot 把当前源码当中 `immortalwrt-mediatek-mt7981-nokia_ea0326gmp-squashfs-factory.bin` 刷入路由器
2. 等待重启之后，用网线连接你的电脑和路由器
3. 打开路由器管理界面`192.168.1.1`，账号是 `root`，密码是 `password`
4. 因为现在很多家庭的光猫默认 IP 也是 `192.168.1.1`，所以我们需要把 NOKIA EA0326GMP 的 IP 改成 `192.168.2.1`，如下图所示：


### 第二步：修改默认的软件源

原文地址：https://help.mirrors.cernet.edu.cn/immortalwrt/

将源改写为如下内容

```conf
src/gz immortalwrt_base https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/base
src/gz immortalwrt_helloworld https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/helloworld
src/gz immortalwrt_kenzo https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/kenzo
src/gz immortalwrt_luci https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/luci
src/gz immortalwrt_packages https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/packages
src/gz immortalwrt_passwall https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/passwall
src/gz immortalwrt_routing https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/routing
src/gz immortalwrt_telephony https://mirrors.cernet.edu.cn/immortalwrt/releases/21.02-SNAPSHOT/packages/aarch64_cortex-a53/telephony
```

### 第三步：安装 OpenClash

> 注：如果你有需求可以自行安装 openclash 最新版本 https://github.com/vernesong/OpenClash/releases

上传本文提供的 ipk 文件，不出意外应该能安装成功，这里需要注意，这个固件安装成功之后不会立刻出现在左侧的服务栏下面，建议你直接重启路由器，然后重新登录，到服务栏里面找一下。

### 第四步：配置 openclash 

导入你自己的订阅或者你自己手写的配置文件，配好代理，尝试启动，

这里会有一个问题，openclash 在第一次启动的时候实际上是去重新下载几个内核文件，但是这些内核文件在 GitHub 上，很容易因为某些众所周知的原因无法下载，这个时候你注意查看安装日志，会发现如下错误：

> 最新版本日志出现：【/tmp/openclash_last_version】下载失败 【curl: (60) SSL certificate problem: self signed certificate More details here: https://curl.haxx.se/docs/sslcerts.html  curl failed to verify the legitimacy of the server and therefore could not establish a secure connection to it. To learn more about this situation and how to fix it, please visit the web page mentioned above

此时你只需要去修改 Github cdn 即可，如下图：

### 第四步：配置 openclash 

重新刷新订阅/或者尝试手动启动，完全按照以上步骤就可以完美启动。
