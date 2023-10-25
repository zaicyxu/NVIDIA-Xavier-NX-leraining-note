# Jetson NX update CMake

如果在Jetson设备上更新特定版本的CMake，可以尝试以下步骤：

1. 首先，确保Jetson设备已连接到网络。
2. 打开终端，运行以下命令来安装CMake的依赖项：
    
    ```bash
    sudo apt-get update
    sudo apt-get install -y libssl-dev
    ```
    
3. 接下来，可以通过以下命令下载并编译所需版本的CMake。在这个例子中，使用版本3.27.2作为示例：
    
    ```bash
    
    wget https://github.com/Kitware/CMake/releases/download/v3.27.2/cmake-3.27.2.tar.gz
    tar -xzvf cmake-3.27.2.tar.gz
    cd cmake-3.27.2
    ./bootstrap
    ```
    
    然后用nproc查看内核个数
    
    ```ruby
    nproc
    
    ```
    
    nx内核是几， make -j后面就是几。
    
    比如，如果nproc显示4，那么命令如下：
    
    ```go
    make -j4
    sudo make install
    
    ```
    
    这将下载CMake源代码，解压缩并编译安装。如果需要其他版本，只需替换上述URL中的版本号。
    
4. 安装完成后，可以使用以下命令验证CMake是否已成功更新到指定版本：
    
    ```bash
    cmake --version
    ```
    

请注意，编译CMake可能需要一些时间和资源。确保Jetson设备具有足够的磁盘空间和计算资源来完成编译过程。

如果只想更新现有的CMake版本而不编译新版本，可以尝试使用以下命令：

```bash
sudo apt-get update
sudo apt-get install --only-upgrade cmake
```

请根据需求选择适当的方法来更新CMake。