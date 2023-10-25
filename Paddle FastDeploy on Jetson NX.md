# Paddle FastDeploy on Jetson NX

### 升级Jetpack:

1. 在文本编辑器中打开 apt 源配置文件，例如：

```
$ sudo vi /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
```

1. 在 deb 命令中更改存储库名称和下载 URL。

原始命令：

```
deb https://repo.download.nvidia.com/jetson/common <release> main
deb https://repo.download.nvidia.com/jetson/<platform> <release> main
```

其中：

- 是要升级到的次要版本的版本号。例如，要升级到次要版本 32.6.1，请将 r32 替换为 32.6。OTA 升级到指定次要版本（在JetPack 4.6中为 r32.6.1）的最新版本。
- 标识平台的处理器：
- t186 用于 Jetson TX2 系列
- t194 / t199 for Jetson AGX Xavier 系列或 Jetson Xavier NX
- t210 用于 Jetson Nano 设备或 Jetson TX1

例如，如果当前版本是 r32.5，而您的平台是 Jetson Xavier NX，则命令将为：

```
deb https://repo.download.nvidia.com/jetson/common r32.6 main
deb https://repo.download.nvidia.com/jetson/ t194 r32.6 main
```

1. 在 **`vi`** 编辑器中，使用方向键移动光标到要修改的位置，按下 **`i`** 键进入编辑模式。然后进行修改。
2. 修改完成后，按下 **`Esc`** 键退出编辑模式，然后输入 **`:wq`** 并按下 **`Enter`** 键，以保存修改并退出 **`vi`** 编辑器。
3. 保存并关闭源配置文件。
4. 输入命令：

```
$ sudo apt update
```

```
$ sudo apt dist-upgrade
```

如果 apt 提示您选择配置文件，请回复 Y 为 yes（以使用该文件的 NVIDIA 更新版本）。

1. 查看 JetPack版本（如 jtop），为4.6.1则完成，如为4.6则再次执行`[1]`操作更新到4.6.1
2. 升级完成后，重新启动 Jetson 设备。

### FastDeply部署

编译过程同样需要满足

- gcc/g++ >= 5.4(推荐8.2)
- cmake >= 3.25.2 （需要cmake最新版本，下载教程链接如下：[https://www.notion.so/Jetson-NX-update-CMake-14819762b67943d5a77c6ae7b6079577?pvs=4](https://www.notion.so/Jetson-NX-update-CMake-14819762b67943d5a77c6ae7b6079577?pvs=21))
- jetpack >= 4.6.1
- python >= 3.6

Python打包依赖`wheel`，编译前请先执行`pip install wheel`

所有编译选项通过环境变量导入

```
git clone https://github.com/PaddlePaddle/FastDeploy.git
cd FastDeploy/python
export BUILD_ON_JETSON=ON
export ENABLE_VISION=ON

# ENABLE_PADDLE_BACKEND & PADDLEINFERENCE_DIRECTORY为可选项
export ENABLE_PADDLE_BACKEND=OFF
export PADDLEINFERENCE_DIRECTORY=/Download/paddle_inference_jetson

sudo python3 setup.py build
sudo python3 setup.py bdist_wheel
```

此过程如果报：

```jsx
error copying directory from"/home/ailab/FastDeploy/pyhton/.setuptools-cmake-build/third_libs/install" to "/home/ailab/FastDeploy/python/fastdeploy/libs/third_libs".

...

subprocess.CalledProcessError: command '['/usr/local/bin/cmake', '--build', '.', '--', '-j', '2']' returned non-zero exit status 2
```

错误如图所示：

![Untitled](Paddle%20FastDeploy%20on%20Jetson%20NX%20dec7fbf6ed3146998e6c90e18e588c5c/Untitled.png)

其错误原因是export的环境变量并没有执行：

![Untitled](Paddle%20FastDeploy%20on%20Jetson%20NX%20dec7fbf6ed3146998e6c90e18e588c5c/Untitled%201.png)

解决方法如下：

1. 打开FastDeploy/python下面的setup.py文件，在最开头加入：

```jsx
import os
os.environ['ENABLE_ORT_BACKEND'] ="ON"
os.environ['BUILD_PADDLE2ONNX'] ="ON"
```

1. 直接运行：

```jsx
sudo python3 setup.py build
sudo python3 setup.py bdist_wheel
```

即可解决问题。

编译完成即会在`FastDeploy/python/dist`目录下生成编译后的`wheel`包，直接pip install即可

（注意，此步骤可能会将.whl文件识别为.zip，此时是无法下载安装的，需要：

```jsx
sudo unzip filename.whl
```

之后将解压的文件夹移动到home/miniforge-pypy3/lib/python3.x/site-packages中，即可，但是，此方法无法自动下载相关依赖，有待后续更新解决方法。

### 第三种方法：

如果出现： "fastdeploy" error: the following arguments are required: tools

按照以下网址下载.whl文件，移动至jetson，pip安装。

网址如下：[https://www.paddlepaddle.org.cn/whl/fastdeploy.html](https://www.paddlepaddle.org.cn/whl/fastdeploy.html)

或者直接运行：

```jsx
pip3 install fastdeploy-gpu-python -f https://www.paddlepaddle.org.cn/whl/fastdeploy.html
```