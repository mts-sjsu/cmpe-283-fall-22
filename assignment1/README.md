# CMPE 283 Fall 2022 Assignment 1

## Team
I did this assignment on my own.






## Steps
1. Create a GCP instance using ubuntu 22.04 provided by GCP
   1. Make sure to enable nested virtualization
2. Install required modules
  ```shell
  > sudo apt install gcc make
  > sudo apt-get linux-headers-$(uname -r) #this might not be necessary
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
7. Results:
```
CMPE 283 Assignment 1 Module Start
Pinbased Controls MSR: 0x3f00000016
  External Interrupt Exiting: Can set=Yes, Can clear=Yes
  NMI Exiting: Can set=Yes, Can clear=Yes
  Virtual NMIs: Can set=Yes, Can clear=Yes
  Activate VMX Preemption Timer: Can set=No, Can clear=Yes
  Process Posted Interrupts: Can set=No, Can clear=Yes
Procbased Controls MSR: 0x3f00000016
  Interrupt-window Exiting: Can set=Yes, Can clear=No
  Use TSC Offsetting: Can set=Yes, Can clear=Yes
  HLT Exiting: Can set=No, Can clear=Yes
  INVLPG Exiting: Can set=No, Can clear=Yes
  MWAIT Exiting: Can set=No, Can clear=Yes
  RDPMC Exiting: Can set=No, Can clear=Yes
  RDTSC Exiting: Can set=No, Can clear=Yes
  CR3-load Exiting: Can set=No, Can clear=Yes
  CR3-store Exiting: Can set=No, Can clear=Yes
  Activate Tertiary Controls: Can set=No, Can clear=Yes
  CR8-load Exiting: Can set=No, Can clear=Yes
  CR8-store Exiting: Can set=No, Can clear=Yes
  Use TPR Shadow: Can set=No, Can clear=Yes
  NMI-window Exiting: Can set=No, Can clear=Yes
  MOV-DR Exiting: Can set=No, Can clear=Yes
  Unconditional I/O Exiting: Can set=No, Can clear=Yes
  Use I/O Bitmaps: Can set=No, Can clear=Yes
  Monitor Trap Flag: Can set=No, Can clear=Yes
  Use MSR Bitmaps: Can set=No, Can clear=Yes
  MONITOR Exiting: Can set=No, Can clear=Yes
  PAUSE Exiting: Can set=No, Can clear=Yes
  Activate Secondary Controls: Can set=No, Can clear=Yes
Exit Controls MSR: 0x3f00000016
  Save Debug Controls: Can set=Yes, Can clear=No
  Host Addresss-space Size: Can set=No, Can clear=Yes
  Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
  Acknowledge Interrupt on Exit: Can set=No, Can clear=Yes
  Save IA32_PAT: Can set=No, Can clear=Yes
  Load IA32_PAT: Can set=No, Can clear=Yes
  Save IA32_EFER: Can set=No, Can clear=Yes
  Load IA32_EFER: Can set=No, Can clear=Yes
  Save VMX-preemption Timer Value: Can set=No, Can clear=Yes
  Clear IA32_BNDCFGS: Can set=No, Can clear=Yes
  Conceal VMX from PT: Can set=No, Can clear=Yes
  Clear IA32_RTIT_CTL: Can set=No, Can clear=Yes
  Clear IA32_LBR_CTL: Can set=No, Can clear=Yes
  Load CET State: Can set=No, Can clear=Yes
  Load PKRS: Can set=No, Can clear=Yes
  Save IA32_PERF_GLOBAL_CTL: Can set=No, Can clear=Yes
  Activate Secondary Controls: Can set=No, Can clear=Yes
Entry Controls MSR: 0x3f00000016
  Load Debug Controls: Can set=Yes, Can clear=No
  IA-32e Mode Guest: Can set=No, Can clear=Yes
  Entry to SMM: Can set=No, Can clear=Yes
  Deactivate dual-monitor treatment: Can set=No, Can clear=Yes
  Load IA32_PERF_GLOBAL_CTRL: Can set=No, Can clear=Yes
  Load IA32_PAT: Can set=No, Can clear=Yes
  Load IA32_EFER: Can set=No, Can clear=Yes
  Load IA32_BNDCFGS: Can set=No, Can clear=Yes
  Conceal VMX from PT: Can set=No, Can clear=Yes
  Load IA32_RTIT_CTL: Can set=No, Can clear=Yes
  Load CET State: Can set=No, Can clear=Yes
  Load Guest IA32_LBR_CTL: Can set=No, Can clear=Yes
  Load Load PKRS: Can set=No, Can clear=Yes

```