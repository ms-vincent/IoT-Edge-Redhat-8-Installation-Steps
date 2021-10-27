# Instructions for Installing Azure IoT Edge 1.1 on Redhat Enterprise Linux 8.x

The following instructions have been updated to include the latest Microsoft provided Moby packages for Redhat 8. Old instructions to install IoT Edge with the 
Moby packages for CentOS 7 is at the following [link](./CentOS7.md). 

1) Microsoft has created a new convenience package to set up the Microsoft repository for a device. To download that package: <BR>
```wget https://packages.microsoft.com/config/rhel/8/packages-microsoft-prod.rpm  ```

2) Install packages including moby for Redhat 8: <BR>
```
sudo yum install ./packages-microsoft-prod.rpm
sudo yum install moby-engine 
sudo yum install moby-cli
sudo yum install moby-buildx
```
  
3) Install openSSL: <BR>
```
sudo yum install -y compat-openssl10
```
  
4)	Register your IoT Edge device in IoT Hub as per instructions: <BR>
https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device?view=iotedge-2018-06&tabs=azure-portal

5)	Edit the config.yaml file to configure your IoT Edge device: <BR>
https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?view=iotedge-2018-06#provision-the-device-with-its-cloud-identity

6)	Restart the IoT Edge service: <BR>
```sudo systemctl restart iotedge```

7)	Check to see that the edge service is running and healthy<BR>
```sudo systemctl status iotedge```

8)	Use the check tool to verify configuration and connection status of the device.<BR>
```sudo iotedge check```
	
9) 	The IoT Edge Agent isn't set to start automatically on boot so you'll need to run the following: <BR>
```sudo systemctl enable iotedge.service```
	
	The agent should auto-start the next time that you reboot/start up your edge device. 
	
10)	Deploy modules and off you go! 
