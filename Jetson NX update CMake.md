# Jetson NX update CMake

If you are updating a specific version of CMake on your Jetson device, you can try the following steps:

1. First, make sure the Jetson device is connected to the network.
2. Open a terminal and run the following command to install CMake dependencies:
    
     ```bash
     sudo apt-get update
     sudo apt-get install -y libssl-dev
     ```
    
3. Next, you can download and compile the required version of CMake with the following command. In this example, version 3.27.2 is used as an example:
    
     ```bash
    
     wget https://github.com/Kitware/CMake/releases/download/v3.27.2/cmake-3.27.2.tar.gz
     tar -xzvf cmake-3.27.2.tar.gz
     cd cmake-3.27.2
     ./bootstrap
     ```
    
     Then use nproc to check the number of cores
    
     ```ruby
     nproc
    
     ```
    
     The number of nx kernel is the number followed by make -j.
    
     For example, if nproc displays 4, the command is as follows:
    
     ```go
     make -j4
     sudo make install
    
     ```
    
     This will download the CMake source code, unzip it and compile it for installation. If you need another version, just replace the version number in the above URL.
    
4. After the installation is complete, you can use the following command to verify whether CMake has been successfully updated to the specified version:
    
     ```bash
     cmake --version
     ```
    

Please note that compiling CMake may require some time and resources. Make sure the Jetson device has enough disk space and computing resources to complete the compilation process.

If you just want to update an existing CMake version without compiling a new version, you can try using the following command:

```bash
sudo apt-get update
sudo apt-get install --only-upgrade cmake
```

Please choose the appropriate method to update CMake according to your needs.
