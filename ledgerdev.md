## Ledger Development

https://ledger.readthedocs.io/en/latest/userspace/getting_started.html

https://github.com/LedgerHQ/blue-devenv/tree/master

### Setup folder for dev
```
mkdir ledgerdev
cd ledgerdev
```

### Getting compilers
A standard ARM gcc to build the non-secure (STM32) firmware and link the secure (ST31) applications
https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads
```
wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2019q4/gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2?revision=108bd959-44bd-4619-9c19-26187abf5225&la=en&hash=E788CE92E5DFD64B2A8C246BBA91A249CB8E2D2D
tar -xf gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2
```

A standard ARM clang above 7.0.0 with ROPI support to build the secure (ST31) applications
https://releases.llvm.org/download.html
```
wget https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
tar -xf clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
```

### Add compilers to PATH
```
// .profile
# GCC
PATH=~/ledgerdev/gcc-arm-none-eabi-9-2019-q4-major/bin:$PATH

# Clang
PATH=~/ledgerdev/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04/bin:$PATH
```

Cross compilation headers are required and provided within the gcc-multilib and g++-multilib packages. To install them on a debian system:
```
sudo apt install gcc-multilib g++-multilib
```

### Download the SDK
https://github.com/LedgerHQ/nanos-secure-sdk/releases
you need to get the version matching your ledger 

This should be a git clone with a checkout of the relevant tag relating to the version on your ledger
```
git clone git@github.com:LedgerHQ/nanos-secure-sdk.git
cd nanos-secure-sdk
git checkout nanos-go-1601
```
link the environment variable `BOLOS_SDK` to the SDK you downloaded.
```
// .profile
export BOLOS_SDK=~/ledgerdev/nanos-secure-sdk
```

### Setup Python Loader
https://github.com/LedgerHQ/blue-loader-python
```
sudo apt install python3-venv python3-dev libudev-dev libusb-1.0-0-dev

virtualenv ledger
source ledger/bin/activate
pip install ledgerblue

```

### Giving permissions on udev

```
sudo vim /etc/udev/rules.d/
SUBSYSTEMS=="usb", ATTRS{idVendor}=="2c97", ATTRS{idProduct}=="0000", MODE="0660", TAG+="uaccess", TAG+="udev-acl" OWNER="<UNIX username>"
SUBSYSTEMS=="usb", ATTRS{idVendor}=="2c97", ATTRS{idProduct}=="0001", MODE="0660", TAG+="uaccess", TAG+="udev-acl" OWNER="<UNIX username>"
SUBSYSTEMS=="usb", ATTRS{idVendor}=="2c97", ATTRS{idProduct}=="0004", MODE="0660", TAG+="uaccess", TAG+="udev-acl" OWNER="<UNIX username>"
```

### Sample apps to run on ledger
https://github.com/LedgerHQ/ledger-sample-apps

```
git clone git@github.com:LedgerHQ/ledger-sample-apps.git
```

### Boilerplate
```
git clone https://github.com/LedgerHQ/ledger-app-boilerplate.git
cd ledger-app-boilerplate/
make load
```
