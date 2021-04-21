# Instructions for Install Azure IoT Edge on Redhat 8

These are unofficial instructions that outline the steps to get Azure IoT Edge 1.1 LTS installed and running on Redhat 8.x. 

In particular, the configuration that I was able to get installed:

- Azure IoT Edge: 1.1.2 
- Red Hat Enterprise Linux 8.2 (deployed as a VM in Azure from the Azure Marketplace: <BR>
Create a resource and select the following tile: <BR>
	![RedhatLVMTile](https://user-images.githubusercontent.com/16802088/115578149-07d19500-a293-11eb-90e2-3c9693cba6cb.jpg) <BR>
Under "Image", select _Red Hat Enterprise Liux 8.2 (LVM) - Gen1_: BR>
	![Redhat82Image](https://user-images.githubusercontent.com/16802088/115578190-10c26680-a293-11eb-91aa-32178123fd02.jpg)<BR><BR>
  If you are using an existing Linux image, you'll have to remove any conflict container packages such as docker, podman, etc. 
<BR><BR>
  
**NOTE**: Redhat is not a tier 1 supported operating system but IoT Edge has been tested to run on Redhat 7.5. Redhat 7.5 specifically is listed as a tier 2 OS as per the platform support documentation and further tests of version 8.x has not been specifically done. Based on my testing, IoT Edge on RHEL 8 seems to work but I have not done extensive testing and your results may vary. <BR><BR>
For a list of supported operating systems, see https://docs.microsoft.com/en-us/azure/iot-edge/support?view=iotedge-2020-11
<BR><BR>

Here are the steps to getting IoT Edge installed:
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
```sudo wget http://packages.microsoft.com/centos/7/prod/moby-cli-20.10.6%2Bazure-1.x86_64.rpm
sudo wget http://packages.microsoft.com/centos/7/prod/moby-engine-20.10.6%2Bazure-1.el7.x86_64.rpm 
sudo wget http://packages.microsoft.com/centos/7/prod/moby-containerd-1.4.4%2Bazure-1.el7.x86_64.rpm
sudo wget http://packages.microsoft.com/centos/7/prod/moby-runc-1.0.0~rc93%2Bazure-1.x86_64.rpm
sudo wget http://packages.microsoft.com/centos/7/prod/moby-buildx-0.5.1%2Bazure-1.x86_64.rpm 
```

  *	Download libiothsm and IoT Edge 
```sudo wget https://github.com/Azure/azure-iotedge/releases/download/1.1.1/libiothsm-std_1.1.1-1.el7.x86_64.rpm
sudo wget https://github.com/Azure/azure-iotedge/releases/download/1.1.1/iotedge-1.1.1-1.el7.x86_64.rpm
```

3)	Install moby packages and IoT Edge

```sudo yum install moby-buildx-0.5.1+azure-1.x86_64.rpm 
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

9)	Deploy modules and off you go! 
 



