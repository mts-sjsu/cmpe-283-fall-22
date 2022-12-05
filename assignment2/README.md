# CMPE 283 Fall 2022 Assignment 2

## Team
I did this assignment on my own.






## Steps
1. Create a GCP instance using ubuntu 22.04 provided by GCP
   1. Make sure to enable nested virtualization

2. Install required modules
  ```shell
  > sudo apt-get update
  > sudo apt-get install gcc make
  > sudo apt-get install flex bison libssl-dev libelf-dev # Required for building linux
  > sudo apt-get install 
  ```
3. Compile linux source code
```shell
> sudo make oldconfig
> sudo make 
> sudo make modules
> sudo make modules_install
> sudo make install
```

4. Host guest VM
```shell
> sudo apt-get install libvirt-daemon-system libvirt-clients virtinst bridge-utils cpu-checker


> virt-install  --network bridge:virbr0 --name guest1 \
 --os-variant=centos7.0 --ram=1024 --vcpus=1  \
 --disk path=/var/lib/libvirt/images/guest1-os.qcow2,format=qcow2,bus=virtio,size=5 \
  --graphics none  --location=/home/mute/CentOS-7-x86_64-DVD-2009.iso \
  --extra-args="console=tty0 console=ttyS0,115200"  --check all=off


```