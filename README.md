# Keystone-with-Docker-configurations-as-non-docker
These are the steps to build keystone as non-docker which can run cpp files and have the docker configurations.
# 1. Clone the Repo
```
git clone --recursive https://github.com/keystone-enclave/keystone.git
cd keystone
git checkout 4e96652
```
without the checkout, latest version of keystone is cloned so make sure to use checkout to clone docker configuration keystone
# 2. Install Dependencies
```
sudo apt update
sudo apt install ninja-build
sudo apt install autoconf automake autotools-dev bc \
bison build-essential curl expat libexpat1-dev flex gawk gcc git \
gperf libgmp-dev libmpc-dev libmpfr-dev libtool texinfo tmux \
patchutils zlib1g-dev wget bzip2 patch vim-common lbzip2 python3 \
pkg-config libglib2.0-dev libpixman-1-dev libssl-dev screen \
device-tree-compiler expect makeself unzip cpio rsync cmake p7zip-full
```
# 3. Setup all environment variables
```
./fast-setup.sh
source source.sh
mkdir build
cd build
cmake ..
make
make image
```
# 4. To build the package
In your build directory:
```
make hello-package
cp examples/hello/hello.ke ./overlay/root
make image
./scripts/run-qemu.sh
```
Result should show lines:
Welcome to Buildroot
```
buildroot login:
```
Login as `root` with the password `sifive`.
You can exit QEMU by `ctrl-a + x` or using `poweroff` command.
# 5. To run hello world
```
insmod keystone-driver.ko
./hello.ke
```
