# Instructions for Installing Azure IoT Edge 1.2 on Redhat Enterprise Linux 8.x

1.	One of the key pre-requisites to run moby is container-selinux. <BR>
Update your RHEL install to the latest version. <BR><BR>
a.	Check to see if container-selinux is installed:<BR>
```rpm -q container-selinux```<BR>
b.	Install container-selinux:<BR>
```sudo yum install container-selinux```<BR>
(the version I had installed at the time of writing was 2:2.124.0.1  )

2.	Download moby packages from the Microsoft repo. 
```
wget https://packages.microsoft.com/centos/7/prod/moby-engine-20.10.6%2Bazure-1.el7.x86_64.rpm 
wget https://packages.microsoft.com/centos/7/prod/moby-cli-20.10.6%2Bazure-1.x86_64.rpm 
wget https://packages.microsoft.com/centos/7/prod/moby-containerd-1.3.9%2Bazure-1.x86_64.rpm 
wget https://packages.microsoft.com/centos/7/prod/moby-runc-1.0.0~rc93%2Bazure-1.x86_64.rpm 
wget http://packages.microsoft.com/centos/7/prod/moby-buildx-0.5.1%2Bazure-1.x86_64.rpm
```
  
3.	Install the downloaded packages in the correct order. Be sure to run each yum install individually:
```
sudo yum install moby-buildx-0.5.1+azure-1.x86_64.rpm 
sudo yum install moby-runc-1.0.0~rc93+azure-1.x86_64.rpm 
sudo yum install moby-containerd-1.3.9+azure-1.x86_64.rpm 
sudo yum install moby-engine-20.10.6+azure-1.el7.x86_64.rpm 
sudo yum install moby-cli-20.10.6+azure-1.x86_64.rpm 
```
  
4.	Install openssl <BR>
```sudo yum install -y compat-openssl10 ```
  
5.	Download Azure IoT Edge 1.2 RPMs 
```
wget https://github.com/Azure/azure-iotedge/releases/download/1.2.0/aziot-edge-1.2.0-1.el7.x86_64.rpm 
wget https://github.com/Azure/azure-iotedge/releases/download/1.2.0/aziot-identity-service-1.2.0-1.x86_64.rpm 
```
  
6.	Install Azure IoT Edge packages 
```
sudo yum install aziot-identity-service-1.2.0-1.x86_64.rpm 
sudo yum install aziot-edge-1.2.0-1.el7.x86_64.rpm 
```

7. Register your IoT Edge device in IoT Hub as per instructions: <BR>
  https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device?view=iotedge-2020-11&tabs=azure-portal <BR>
  
8. Continue the installation by provisioning the device with the cloud identity: <BR>
  https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?view=iotedge-2020-11#provision-the-device-with-its-cloud-identity 
  
9. Deploy modules and off you go!
