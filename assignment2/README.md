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
3. Collect required files
   Copy both `cpuid.c` and `vmx.c` to corresponding location in linux 

```shell
> cp cpuid.c ~/linux/arch/x86/kvm
> cp vmx.c ~/linx/arch/x86/kvm/vmx
```

4. Compile linux source code
```shell
> sudo make oldconfig
> sudo make 
> sudo make modules
> sudo make modules_install
> sudo make install
```

1. Host guest VM
Create a default config file `ubuntu_config` for the ubuntu image:
```text
password: ubuntu
ssh_pwauth: True
chpasswd: { expire: False }
```


```shell
> sudo apt-get install qemu-kvm cloud-image-utils
> cloud-localds guest.img ubuntu_config
> sudo qemu-system-x86_64 -enable-kvm -hda bionic.img -drive "file=guest.img,format=raw" -m 1024 -display curses -nographic

```