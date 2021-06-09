# Instructions for Installing Azure IoT Edge 1.1 on Redhat Enterprise Linux 8.x

1)	One of the key pre-requisites to run moby is container-selinux. <BR>
   Update your RHEL install to the latest version. 
   * Check to see if container-selinux is installed:<BR>
	```rpm -q container-selinux```
   *	Install container-selinux:<BR>
```sudo yum install container-selinux```<BR>
(the version I had installed at the time of writing was 2:2.124.0.1)
2)	Download all the packages required for the installing of IoT Edge. <BR>
(the moby packages that I downloaded and installed are what’s required for Azure IoT Edge 1.1.x so if you try to install other versions, the package requirements may vary)
  
  * Download Moby packages
```
sudo wget http://packages.microsoft.com/centos/7/prod/moby-cli-20.10.6%2Bazure-1.x86_64.rpm
sudo wget http://packages.microsoft.com/centos/7/prod/moby-engine-20.10.6%2Bazure-1.el7.x86_64.rpm 
sudo wget http://packages.microsoft.com/centos/7/prod/moby-containerd-1.4.4%2Bazure-1.el7.x86_64.rpm
sudo wget http://packages.microsoft.com/centos/7/prod/moby-runc-1.0.0~rc93%2Bazure-1.x86_64.rpm
sudo wget http://packages.microsoft.com/centos/7/prod/moby-buildx-0.5.1%2Bazure-1.x86_64.rpm 
```

  *	Download libiothsm and IoT Edge 
```
sudo wget https://github.com/Azure/azure-iotedge/releases/download/1.1.1/libiothsm-std_1.1.1-1.el7.x86_64.rpm
sudo wget https://github.com/Azure/azure-iotedge/releases/download/1.1.1/iotedge-1.1.1-1.el7.x86_64.rpm
```

3)	Install moby packages and IoT Edge

```
sudo yum install moby-buildx-0.5.1+azure-1.x86_64.rpm 
sudo yum install moby-runc-1.0.0~rc93+azure-1.x86_64.rpm
sudo yum install moby-containerd-1.4.4+azure-1.el7.x86_64.rpm 
sudo yum install moby-engine-20.10.6+azure-1.el7.x86_64.rpm
sudo yum install moby-cli-20.10.6+azure-1.x86_64.rpm
sudo yum install libiothsm-std_1.1.1-1.el7.x86_64.rpm 
sudo yum install iotedge-1.1.1-1.el7.x86_64.rpm
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
