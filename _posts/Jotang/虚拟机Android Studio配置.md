## 虚拟机Android Studio配置

### 1.安装Android Studio

在Ubuntu Software中搜索Android Studio下载即可。打开后选择Do Not Import Settings。

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413092547292.png" alt="image-20230413092547292" style="zoom:67%;" />

第一次打开大概率会弹出界面说明没有安装SDK，选择cancel即可。随后进入安装向导

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413092711353.png" alt="image-20230413092711353" style="zoom: 67%;" />

一路next即可。中途会提示阅读接受条款，最后开始安装

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413093018401.png" alt="image-20230413093018401" style="zoom:67%;" />

最后跳转至此页面，安装成功

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413093116936.png" alt="image-20230413093116936" style="zoom:67%;" />

### 2.安装并配置额外的SDK

> 为什么需要安装额外的SDK？
>
> 市面上手机安装的安卓版本参差不齐，为了保证需求和测试机环境，需要更多SDK支持

在File-Settings中打开设置

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413094024178.png" alt="image-20230413094024178" style="zoom:67%;" />

Appearance&Behavoir-System Settings-Android SDK，安装需要的SDK

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413094047065.png" alt="image-20230413094047065" style="zoom:67%;" />

进入下载页面

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413094419691.png" alt="image-20230413094419691" style="zoom:67%;" />

#### 2.1 对于AMD电脑

由于电脑cpu是AMD的，不支持硬件快速加速，也就无法运行AS自带的模拟器，需要自己配置。再进入Andriod SDK，选择如下SDK包

<img src="https://gitee.com/Cisco-F/image/raw/master/Android%20Studio/image-20230413095112714.png" alt="image-20230413095112714" style="zoom:67%;" />



