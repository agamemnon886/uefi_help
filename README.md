# uefi_help
Getting started with EDK2 in Linux, hello world


1) Download EDK2
```
$ git clone https://github.com/tianocore/edk2.git
$ cd edk2
$ git submodule update --init --recursive
```
2) Install nasm and uuid-dev
```
$ sudo apt-get install uuid-dev nasm libuuid libuuid-dev
```
3) Build tools
```
$ source edksetup.sh

$ make -C BaseTools
```
4) Configure build environment

Open "Conf/target.txt" and change ACTIVE_PLATFORM and TARGET_ARCH:
```
TARGET_ARCH           = X64
ACTIVE_PLATFORM       = OvmfPkg/OvmfPkgX64.dsc
```
5) Create "hello" directory in edk2 root directory and copy "hello.c" and "hello.inf" into "hello" directory.

6) Add "hello" to "OvmfPkg/OvmfPkgX64.dsc" into section "Components":
```
[Components]                                                                                                           
   hellow/hello.inf
```

7) Build firmware image:
```
$ cd edk2
$ build
```
8) Run QEMU
```
$ cd /edk2/Build/OvmfX64/DEBUG_GCC5/FV
$ mkdir hda-contents
$ cp ../X64/hellow.efi hda-contents/
$ qemu-system-x86_64 -L . --bios OVMF.fd -hda fat:64:rw:hda-contents -net none
```
9) In UEFI shell input the following commands:
```
Shell> fs0:
FS0:\> hello.efi
Hello World
```



