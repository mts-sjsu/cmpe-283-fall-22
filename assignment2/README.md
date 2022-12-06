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
  > sudo apt-get install flex bison libssl-dev libelf-dev pahole # Required for building linux
  ```
3. Collect required files
Copy the linux kernal into `~/linux` folder, then copy the modified `cpuid.c` and `vmx.c` to their corresponding locations.

```shell
> cp cpuid.c ~/linux/arch/x86/kvm
> cp vmx.c ~/linx/arch/x86/kvm/vmx
```

4. Compile linux source code
   I am using the Linux kernel 5.15.81 found [here](https://www.kernel.org)
```shell
> sudo make oldconfig
# Might need to comment out
> sudo make 
> sudo make modules
> sudo make INSTALL_MOD_STRIP=1 modules_install
> sudo make install
> reboot
```

5. Host guest VM
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

6. Testing Implementation
Once the inner VM is successfully created, log in with `username=ubuntu` and `password=ubuntu`, then install `cpuid` to run the
command
```shell
> sudo apt-get install cpuid
> cpuid -l 0x4FFFFFFC   # Should return exit count in eax
> cpuid -l 0x4FFFFFFD   # Should return vmm cyles in ebx + ecx
```
And in the host/outer VM run
```shell
sudo dmesg
``` 
This should show the newly implemented `printk` message in the host VM detailing the number of exits and number of cycles. 
The screenshot shows the result, where the upper window is the inner VM, and the lower window is the host VM.
