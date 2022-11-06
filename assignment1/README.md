# CMPE 283 Fall 2022 Assignment 1

## Team
I did this assignment on my own.






## Steps
1. Create a GCP instance using ubuntu 22.04 provided by GCP
   1. Make sure to enable nested virtualization
2. Install required modules
  ```shell
  > sudo apt install gcc make
  > sudo apt-get linux-headers-$(uname -r)
  ```
3. Connect the GCP instance with Github
   1. This can be achieved by adding the public key of the instance to Github repository deploy keys. Tutorial [here](https://docs.github.com/en/developers/overview/managing-deploy-keys)
4. `git clone` the repository with ssh
5. Verify the provided code yields expected results
```shell
make
sudo insmod ./cmpe283-1.ko #insert the built module into the Linux Kernel
sudo dmesg #print the kernel ring buffer
```
6. Implement the rest of the MSRs
   1. Pinbased controls: SDM V3, 24.6.1
   2. Procbased controls: SDM V3, 24.6.2
   3. Exit controls: SDM V3, 24.7.1
   4. Entry controls: SDM V3, 24.8.1
   5. Secondary procbased controls: SDM V3, 24.6.2
   6. Tertiary procbased controls: SDM V3, 24.6.2