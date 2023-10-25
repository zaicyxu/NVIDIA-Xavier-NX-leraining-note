# Jetson Xavier NX风扇控制

## **Xavier(Xavier,NX, Nano, AGX Xavier, TX1, TX2)开机启动风扇**

jetson Xavier开机自动启动风扇的方法很简单，不要设置脚本，一个软件搞定。

jetson-stats,jetson-stats是一个用来监控和控制jetson系列（Xavier NX, Nano, AGX Xavier, TX1, TX2）硬件平台的一个软件。

1. **安装 Python**：首先确认您的 Jetson 上已经安装了 Python。您可以在终端中输入以下命令来检查是否已安装 Python：
    
    ```bash
    bashCopy code
    python3 --version
    
    ```
    
    如果系统中没有安装 Python，您需要先安装 Python。使用以下命令安装 Python 3：
    
    ```bash
    bashCopy code
    sudo apt-get update
    sudo apt-get install python3
    
    ```
    
2. **安装 pip**：一旦安装了 Python，您可以安装 Python 包管理工具 **`pip`**。在终端中输入以下命令：
    
    ```bash
    bashCopy code
    sudo apt-get install python3-pip
    
    ```
    
    这将会安装 **`pip`** 并使其可用于 Python 3。
    
3. **验证安装**：安装完成后，您可以在终端中输入以下命令来验证 **`pip`** 是否安装成功：
    
    ```bash
    bashCopy code
    pip3 --version
    
    ```
    

### **1.安装jetson-stats**

```
sudo pip3 install jetson-stats
```

看到如下信息说明安装成功：

![https://www.yahboom.com/Public/ueditor/php/upload/image/20201226/1608970559286499.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20201226/1608970559286499.png)

### **2.启动Jetson-stats**

执行此代码第一遍会报错，因为第一遍需要导入命令，再次执行即可。

```
sudo jtop
```

### 

![7110707ef852a3acb8ada97b6832d780.jpg](Jetson%20Xavier%20NX%E9%A3%8E%E6%89%87%E6%8E%A7%E5%88%B6%20a58cf0d4c58b490fb16f33a97a5ee245/7110707ef852a3acb8ada97b6832d780.jpg)

### **3.设置开机启动风扇**

点击CTRL进入风扇控制界面

按下按键**s**和**e**设置jetson_clocks **Running**和boot **Enable**，如图所示：

![e060283495705e52bfe1c81954d5943b.jpg](Jetson%20Xavier%20NX%E9%A3%8E%E6%89%87%E6%8E%A7%E5%88%B6%20a58cf0d4c58b490fb16f33a97a5ee245/e060283495705e52bfe1c81954d5943b.jpg)

根据自己需求，将Profiles, quiet, cool分别调整到合适的转速。一般50-70较为合适（0%-100%）

点击Quit退出软件。