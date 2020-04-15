# rpi3_virtualization

### Packages Used
Currently only ```virt-install```, which uses ```QEMU``` on the back end, is required.

If more are required, they will be added here.
### Current command to be run
```sudo virt-install --name Fedora_31_AArch64 --ram 1024 --arch aarch64 --disk size=8 --os-variant fedora28 --location https://dl.fedoraproject.org/pub/fedora/linux/releases/31/Everything/aarch64/os/ --extra-args "inst.ks=https://pwhalen.fedorapeople.org/kickstarts/Fedora-Minimal-AArch64.ks" --machine raspi3 --boot uefi --vcpus=4```

This of course implies that the links provided continue to work. Further, this kickstart in use was from an out-of-date guide on building an ARM64 virtualization for Fedora, not specific to the rasberrypi3. The hope is that there is enough crossover to be viable.

### Bugs:

Currently, I haven't parsed out what this error is suggesting; KVM is enabled on the host machine this is being tested on.

```Starting install...
Retrieving file vmlinuz...                                  |  25 MB  00:01 !!! 
Retrieving file initrd.img...                               |  65 MB  00:05     
Allocating 'Fedora_31_AArch64-2.qcow2'                      | 8.0 GB  00:00     
ERROR    internal error: process exited while connecting to monitor: qemu-system-aarch64: /builddir/build/BUILD/qemu-4.1.1/exec.c:899: cpu_address_space_init: Assertion `asidx == 0 || !kvm_enabled()' failed.
Removing disk 'Fedora_31_AArch64-2.qcow2'                   |    0 B  00:00     
Domain installation does not appear to have been successful.
If it was, you can restart your domain by running:
  virsh --connect qemu:///system start Fedora_31_AArch64
otherwise, please restart your installation.```
 
#### Possible solution?
Looks like a security module issue.
```https://bugs.launchpad.net/qemu/+bug/1836501```
