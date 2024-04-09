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
3) Install nasm 2.15
```
	wget http://www.nasm.us/pub/nasm/releasebuilds/2.15.05/nasm-2.15.05.tar.bz2
	tar xfj nasm-2.15.05.tar.bz2
	cd nasm-2.15.05/
	./autogen.sh
	./configure --prefix=/usr/local/ 
	make 
	sudo make install
```
4) Build tools
```
$ cd edk2
$ source edksetup.sh
$ make -C BaseTools
```
5) Configure build environment

Open "Conf/target.txt" and change ACTIVE_PLATFORM and TARGET_ARCH:
```
TARGET_ARCH           = X64
ACTIVE_PLATFORM       = OvmfPkg/OvmfPkgX64.dsc
TOOL_CHAIN_TAG        = GCC5
```
6) Create "hello" directory in edk2 root directory and copy "hello.c" and "hello.inf" into "hello" directory.

7) Add "hello" to "OvmfPkg/OvmfPkgX64.dsc" into section "Components":
```
[Components]                                                                                                           
   hellow/hello.inf
```

8) Build firmware image:
```
$ cd edk2
$ build
```
9) Run QEMU
```
$ cd /edk2/Build/OvmfX64/DEBUG_GCC5/FV
$ mkdir hda-contents
$ cp ../X64/hellow.efi hda-contents/
$ qemu-system-x86_64 -L . --bios OVMF.fd -hda fat:64:rw:hda-contents -net none
```
10) In UEFI shell input the following commands:
```
Shell> fs0:
FS0:\> hello.efi
Hello World
```



