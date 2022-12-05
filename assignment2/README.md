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
  ```
3. Compile linux source code
```shell
> sudo make oldconfig
> sudo make 
> sudo make modules
> sudo make modules_install
> sudo make install
```
1. `git clone` the repository with ssh