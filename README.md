# Instructions for Installation of Azure IoT Edge on Redhat 8.x

These are unofficial instructions that outline the steps to get Azure IoT Edge installed and running on Redhat 8.x. 

There were significant changes between IoT Edge 1.1 and 1.2 and as such the instructions to install IoT Edge vary slightly.

The configurations that I was able to get installed and have done basic tests on:

- Azure IoT Edge: 1.1.2 + 1.2.0.1
- Red Hat Enterprise Linux 8.1 and 8.2 (deployed as a VM in Azure from the Azure Marketplace: <BR>
Create a resource and select the following tile: <BR>
	![RedhatLVMTile](https://user-images.githubusercontent.com/16802088/115578149-07d19500-a293-11eb-90e2-3c9693cba6cb.jpg) <BR>
Under "Image", select _Red Hat Enterprise Linux 8.2 (LVM) - Gen1_ or _Red Hat Enterprise Linux 8.1 - Gen1_: <BR>
	![RHEL%2081%2082](https://github.com/ms-vincent/IoT-Edge-Redhat-8-Installation-Steps/blob/main/Images/RHEL%2081%2082.jpg)<BR><BR>
  If you are using an existing Linux image, you'll have to remove any conflicting container packages such as docker, podman, etc. There also might be some other dependencies that you'll need to get installed such as openssl. 
<BR><BR>
  
**NOTE**: Redhat is not a tier 1 supported operating system but IoT Edge has been tested to run on Redhat 7.5. Redhat 7.5 specifically is listed as a tier 2 OS as per the platform support documentation and further tests of version 8.x has not been specifically completed. Based on my testing, IoT Edge on RHEL 8 seems to work but I have not done extensive testing and your results may vary. <BR><BR>
For a list of supported operating systems, see https://docs.microsoft.com/en-us/azure/iot-edge/support?view=iotedge-2020-11
<BR><BR>

## Installation of IoT Edge on Redhat Linux 

**Oct 2021 Update**: The following documentation has been updated to include instructions on how to install Edge using the new Microsoft provided moby packages for Redhat 8. 
	
Follow the instructions for the version of Azure IoT Edge that you are looking to install: 
1) [Azure IoT Edge 1.1 LTS](https://github.com/ms-vincent/IoT-Edge-Redhat-8-Installation-Steps/blob/main/Edge11/README.md)
2) [Azure IoT Edge 1.2](https://github.com/ms-vincent/IoT-Edge-Redhat-8-Installation-Steps/blob/main/Edge12/README.md)

	
 



