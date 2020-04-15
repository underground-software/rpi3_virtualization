# rpi3_virtualization

### Packages Used
Currently only ```virt-install```, which uses ```QEMU``` on the back end, is required.

If more are required, they will be added here.
### Current command to be run
```sudo virt-install        --name Fedora_31_AArch64 --ram 4096 --arch aarch64     --disk size=8 --os-variant fedora28       --location https://dl.fedoraproject.org/pub/fedora/linux/releases/31/Everything/aarch64/os/        --extra-args "inst.ks=https://pwhalen.fedorapeople.org/kickstarts/Fedora-Minimal-AArch64.ks" --machine raspi3 --boot uefi ```
This of course implies that the links provided continue to work. Further, this kickstart in use was from an out-of-date guide on building an ARM64 virtualization for Fedora, not specific to the rasberrypi3. The hope is that there is enough crossover to be viable.

### Bugs:
Currently the command above does now allow for the installation to go through, as it requires 4 CPUs allocated, where as by default it is only being allocated 2.

```Starting install...
Retrieving file vmlinuz...                                  |  25 MB  00:01 !!! 
Retrieving file initrd.img...                               |  65 MB  00:03     
Allocating 'Fedora_31_AArch64-2.qcow2'                      | 8.0 GB  00:02     
ERROR    internal error: process exited while connecting to monitor: 2020-04-15T14:54:38.658077Z qemu-system-aarch64: Invalid SMP CPUs 2. The min CPUs supported by machine 'raspi3' is 4
Removing disk 'Fedora_31_AArch64-2.qcow2'                   |    0 B  00:00     
Domain installation does not appear to have been successful.
If it was, you can restart your domain by running:
  virsh --connect qemu:///system start Fedora_31_AArch64
otherwise, please restart your installation.```