# Paddle FastDeploy on Jetson NX

### Upgrade Jetpack:

1. Open the apt source configuration file in a text editor, for example:

```
$ sudo vi /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
```

1. Change the repository name and download URL in the deb command.

Original command:

```
deb https://repo.download.nvidia.com/jetson/common <release> main
deb https://repo.download.nvidia.com/jetson/<platform> <release> main
```

in:

- <release> is the version number of the minor version to upgrade to. For example, to upgrade to minor version 32.6.1, replace r32 with 32.6. OTA upgrades to the latest version of the specified minor version (r32.6.1 in JetPack 4.6).
-Identifies the platform's processor:
- t186 for Jetson TX2 series
- t194/t199 for Jetson AGX Xavier series or Jetson Xavier NX
- t210 for Jetson Nano devices or Jetson TX1

For example, if the current version is r32.5 and your platform is Jetson Xavier NX, the command would be:

```
deb https://repo.download.nvidia.com/jetson/common r32.6 main
deb https://repo.download.nvidia.com/jetson/ t194 r32.6 main
```

1. In the **`vim`** editor, use the direction keys to move the cursor to the position to be modified, and press the **`i`** key to enter the editing mode. Then make changes.
2. After the modification is completed, press the **`Esc`** key to exit the edit mode, then enter **`:wq`** and press the **`Enter`** key to save the changes and exit**` vi`** editor.
3. Save and close the source configuration file.
4. Enter the command:

```
$ sudo apt update
```

```
$ sudo apt dist-upgrade
```

If apt prompts you to select a configuration file, reply Y to yes (to use the NVIDIA updated version of the file).

1. Check the JetPack version (such as jtop). If it is 4.6.1, it is completed. If it is 4.6, perform the `[1]` operation again to update to 4.6.1
2. After the upgrade is complete, restart the Jetson device.

### FastDeply deployment

The compilation process also needs to meet the

- gcc/g++ >= 5.4 (8.2 recommended)
- cmake >= 3.25.2 (requires the latest version of cmake, the download tutorial link is as follows: [https://www.notion.so/Jetson-NX-update-CMake-14819762b67943d5a77c6ae7b6079577?pvs=4](https://www. notion.so/Jetson-NX-update-CMake-14819762b67943d5a77c6ae7b6079577?pvs=21))
- jetpack >= 4.6.1
- python >= 3.6

Python packaging depends on `wheel`. Please execute `pip install wheel` before compiling.

All compilation options are imported through environment variables

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

If an error occurs during this process:

```jsx
error copying directory from"/home/ailab/FastDeploy/pyhton/.setuptools-cmake-build/third_libs/install" to "/home/ailab/FastDeploy/python/fastdeploy/libs/third_libs".

...

subprocess.CalledProcessError: command '['/usr/local/bin/cmake', '--build', '.', '--', '-j', '2']' returned non-zero exit status 2
```

The error is as shown in the picture:

![image](https://github.com/zaicyxu/NVIDIA-Xavier-NX-leraining-note/assets/106503993/7365433b-6728-43be-a92b-046096863d07)


The reason for the error is that the export environment variable is not executed:

![image](https://github.com/zaicyxu/NVIDIA-Xavier-NX-leraining-note/assets/106503993/dbcd493c-abec-49b4-9031-b68d47177ae0)


The solution is as follows:

1. Open the setup.py file under FastDeploy/python and add at the beginning:

```jsx
import os
os.environ['ENABLE_ORT_BACKEND'] ="ON"
os.environ['BUILD_PADDLE2ONNX'] ="ON"
```

1. Running：

```jsx
sudo python3 setup.py build
sudo python3 setup.py bdist_wheel
```

That will solve the problem.

After compilation is completed, the compiled `wheel` package will be generated in the `FastDeploy/python/dist` directory. Just pip install it.

(Note that this step may recognize the .whl file as .zip, and it cannot be downloaded and installed at this time. You need:

```jsx
sudo unzip filename.whl
```

Then move the decompressed folder to home/miniforge-pypy3/lib/python3.x/site-packages. However, this method cannot automatically download related dependencies, and a solution will be updated later.

### The third method:

If: "fastdeploy" error: the following arguments are required: tools

Follow the following URL to download the .whl file, move it to jetson, and install it with pip.

The URL is as follows: [https://www.paddlepaddle.org.cn/whl/fastdeploy.html](https://www.paddlepaddle.org.cn/whl/fastdeploy.html)

Or run directly:

```jsx
pip3 install fastdeploy-gpu-python -f https://www.paddlepaddle.org.cn/whl/fastdeploy.html
```
