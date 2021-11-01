# Instructions for Installing Azure IoT Edge 1.2 on Redhat Enterprise Linux 8.x 

The following instructions have been updated to include the latest Microsoft provided Moby packages for Redhat 8. Previous instructions to install IoT Edge with the 
Moby packages for CentOS 7 can be found at the following [link](./CentOS7.md). 

1. Microsoft has created a new convenience package to set up the Microsoft repository for a device. To download that package: <BR>
```  wget https://packages.microsoft.com/config/rhel/8/packages-microsoft-prod.rpm  ```

2. Install packages including Moby for Redhat 8: <BR>
```
sudo yum install ./packages-microsoft-prod.rpm
sudo yum install moby-engine 
sudo yum install moby-cli
sudo yum install moby-buildx
```
  
3. Install openSSL: <BR>
```
  sudo yum install -y compat-openssl10
```
  
4.	Download Azure IoT Edge 1.2 RPMs 
```
wget https://github.com/Azure/azure-iotedge/releases/download/1.2.0/aziot-edge-1.2.0-1.el7.x86_64.rpm 
wget https://github.com/Azure/azure-iotedge/releases/download/1.2.0/aziot-identity-service-1.2.0-1.x86_64.rpm 
```
  
5.	Install Azure IoT Edge packages 
```
sudo yum install aziot-identity-service-1.2.0-1.x86_64.rpm 
sudo yum install aziot-edge-1.2.0-1.el7.x86_64.rpm 
```

7. Register your IoT Edge device in IoT Hub as per instructions: <BR>
  https://docs.microsoft.com/en-us/azure/iot-edge/how-to-register-device?view=iotedge-2020-11&tabs=azure-portal <BR>
  
8. Continue the installation by provisioning the device with the cloud identity: <BR>
  https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge?view=iotedge-2020-11#provision-the-device-with-its-cloud-identity 
  
9. The Azure IoT Edge service isn't set to start automatically on boot so you'll need to run the following systemctl commands:
```
sudo systemctl enable aziot-edged.service
sudo systemctl enable aziot-keyd.service
sudo systemctl enable aziot-certd.service
sudo systemctl enable aziot-identityd.service
sudo systemctl enable aziot-tpmd.service
 ```

The edge services should auto-start the next time that you reboot/start up your edge device.  
  
9. Deploy modules and off you go!
