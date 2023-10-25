#JetsonXavierNXFanControl

## **Xavier(Xavier,NX, Nano, AGX Xavier, TX1, TX2) turns on the fan**

The method to automatically start the fan on jetson Xavier is very simple. No need to set up a script, just a software can do it.

jetson-stats, jetson-stats is a software used to monitor and control the jetson series (Xavier NX, Nano, AGX Xavier, TX1, TX2) hardware platform.

1. **Install Python**: First make sure Python is installed on your Jetson. You can check whether Python is installed by entering the following command in the terminal:
    
     ```bash
     bashCopy code
     python3 --version
    
     ```
    
     If Python is not installed on your system, you need to install Python first. Install Python 3 using the following command:
    
     ```bash
     bashCopy code
     sudo apt-get update
     sudo apt-get install python3
    
     ```
    
2. **Install pip**: Once Python is installed, you can install the Python package management tool **`pip`**. Enter the following command in the terminal:
    
     ```bash
     bashCopy code
     sudo apt-get install python3-pip
    
     ```
    
     This will install **`pip`** and make it available for Python 3.
    
3. **Verify installation**: After the installation is complete, you can enter the following command in the terminal to verify whether **`pip`** is installed successfully:
    
     ```bash
     bashCopy code
     pip3 --version
    
     ```
    

### **1.Install jetson-stats**

```
sudo pip3 install jetson-stats
```

If you see the following information, the installation is successful:

![https://www.yahboom.com/Public/ueditor/php/upload/image/20201226/1608970559286499.png](https://www.yahboom.com/Public/ueditor/php/upload/image/20201226 /1608970559286499.png)

### **2. Start Jetson-stats**

An error will be reported the first time you execute this code, because the command needs to be imported the first time, and you can just execute it again.

```
sudo jtop
```

###

![7110707ef852a3acb8ada97b6832d780.jpg](Jetson%20Xavier%20NX%E9%A3%8E%E6%89%87%E6%8E%A7%E5%88%B6%20a58cf0d4c58b490fb16f33a97a5ee245/71 10707ef852a3acb8ada97b6832d780.jpg)

### **3. Set the fan to start at boot**

Click CTRL to enter the fan control interface

Press the keys **s** and **e** to set jetson_clocks **Running** and boot **Enable**, as shown in the figure:

![e060283495705e52bfe1c81954d5943b.jpg](Jetson%20Xavier%20NX%E9%A3%8E%E6%89%87%E6%8E%A7%E5%88%B6%20a58cf0d4c58b490fb16f33a97a5ee245 /e060283495705e52bfe1c81954d5943b.jpg)

According to your own needs, adjust Profiles, quiet, and cool to the appropriate speed respectively. Generally, 50-70 is more suitable (0%-100%)

Click Quit to exit the software.
