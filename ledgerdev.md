## Ledger Development

https://ledger.readthedocs.io/en/latest/userspace/getting_started.html

https://github.com/LedgerHQ/blue-devenv/tree/master

### Setup folder for dev
```
mkdir ledgerdev
cd ledgerdev
sudo apt install gcc-multilib g++-multilib git libusb-1.0-0-dev python python3-pip libudev-dev libtinfo-dev
```

### Getting compilers
A standard ARM gcc to build the non-secure (STM32) firmware and link the secure (ST31) applications
https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads
```
wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2019q4/gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2
tar -xf gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2
```

A standard ARM clang above 7.0.0 with ROPI support to build the secure (ST31) applications
https://releases.llvm.org/download.html
```
wget https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.0/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
tar -xf clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
```
Cross compilation headers are required and provided within the gcc-multilib and g++-multilib packages. To install them on a debian system:
```
sudo apt install gcc-multilib g++-multilib libncurses5
```

### Download the SDK
https://github.com/LedgerHQ/nanos-secure-sdk/releases
you need to get the version matching your ledger 

This should be a git clone with a checkout of the relevant tag relating to the version on your ledger
```
git clone git@github.com:LedgerHQ/nanos-secure-sdk.git
cd nanos-secure-sdk
git fetch --all --tags --prune
git checkout nanos-160
```


### Setup Python Loader
https://github.com/LedgerHQ/blue-loader-python
```
sudo apt install python3-venv python3-dev libudev-dev libusb-1.0-0-dev

python3 -m venv ledger
source ledger/bin/activate
pip install ledgerblue

```

### Add compilers to PATH in the activate script
```
// ledger/bin/activate
...
# GCC
PATH=~/ledgerdev/gcc-arm-none-eabi-9-2019-q4-major/bin:$PATH

# Clang
PATH=~/ledgerdev/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04/bin:$PATH
```

### link the environment variable `BOLOS_SDK` to the SDK you downloaded.
```
// ledgerdev/bin/activate
...
export BOLOS_SDK=~/ledgerdev/nanos-secure-sdk
export GCCPATH=/home/sean/ledgerdev/gcc-arm-none-eabi-9-2019-q4-major/bin/
export CLANGPATH=/home/sean/ledgerdev/clang+llvm-10.0.0-x86_64-linux-gnu-ubuntu-18.04/bin/
//export GCCPATH=$(pwd)/
//export CLANGPATH=$(pwd)/
```

### Giving permissions on udev

```
wget -q -O - https://raw.githubusercontent.com/LedgerHQ/udev-rules/master/add_udev_rules.sh | sudo bash
```

### Test if device communicates

```
python -m ledgerblue.checkGenuine --targetId 0x31100004
```

### Sample apps to run on ledger
https://github.com/LedgerHQ/ledger-sample-apps

```
git clone git@github.com:LedgerHQ/ledger-sample-apps.git
```
### Compile and load
```
make clean && make DEBUG=1 -j12 load
```


### Debugging setup
https://ledger.readthedocs.io/en/latest/userspace/debugging.html

