---
title: Creating GCC and Binutils Cross-Compilers in Ubuntu
date: 2024-02-08 23:12:00 +0900
categories: [Computer Science, System Programming]
tags: [linux, cross-compiler, gcc]     # TAG names should always be lowercase
---
# What is a Cross-Compiler?
A cross-compiler is an essential tool for software development targeting different architectures.
For instance, developers using an x86_64 architectures Ubuntu Linux system may need to develop software for ARM architecture embedded systems or platforms based on other architectures.

Cross-compilers bridge the gap between the development environment and the target environment, enabling application development for various platforms.
This is particularly important in embedded system development, operating system development, and application development targeting diverse architectures.

# Installation Process
Let's examine the process of creating cross-compilers with GCC and Binutils on an Ubuntu system, including post-installation verification and detailed usage examples.

> The versions and commands provided here are subject to change over time, so it's best to check the latest information before starting your work.
{: prompt-warning }

## Installing Necessary Tools and Libraries
```bash
sudo apt update

sudo apt install build-essential bison flex libiconv-hook-dev libtool make patchutils nasm python2 libgmp-dev libmpfr-dev libmpc-dev texinfo gcc-multilib
```
These commands provide the dependencies needed for the compilation process.

## Cross-Compiling GCC and Binutils
### Installing Binutils
```bash
wget https://ftp.gnu.org/gnu/binutils/binutils-2.42.tar.gz
tar -xzvf ./binutils-2.42.tar.gz 

cd binutils-2.42

# Setting up the build directory and compiling 
mkdir build && cd build 

../configure --target=x86_64-pc-linux-gnu --prefix=/usr/cross --enable-64-bit-bfd --disable-shared --disable-nls 

make 

sudo make install

```
* `tar -xzvf`: Unpacks the source code.
* `mkdir build && cd build`: Creates a separate directory for building and moves into it, helping to keep the source directory clean.
* `../configure`: Configures the environment for cross-compilation.
* `make`: Builds the software.
* `sudo make install`: Installs the built software on the system.

### Installing GCC
GCC must also be installed for cross-compilation.

The GCC installation process is similar to Binutils, with the additional step of downloading necessary dependencies by running `./contrib/download_prerequisites`.
```bash
wget https://ftp.gnu.org/gnu/gcc/gcc-13.2.0/gcc-13.2.0.tar.gz
tar -xzvf ./gcc-13.2.0.tar.gz

cd gcc-13.2.0

# Downloading necessary dependencies
./contrib/download_prerequisites

# Setting up the build directory and compiling
mkdir build && cd build

../configure --target=x86_64-pc-linux-gnu --prefix=/usr/cross --disable-nls --enable-languages=c,c++ --without-headers --disable-shared --with-system-zlib

make

sudo make install
```
* `wget`: Downloads the GCC source code.
* `tar -xzvf`: Unpacks the source code.
* `./contrib/download_prerequisites`: Automatically downloads and installs GMP, MPFR, MPC, and other dependencies required for GCC compilation.
* `../configure`: Configures the environment for cross-compilation. The `--enable-languages=c,c++` option activates support for the C and C++ languages.
* `make`: Builds the software.
* `sudo make install`: Installs the built software on the system.

Running `./contrib/download_prerequisites` during the GCC installation process automatically installs additional libraries necessary for a more stable GCC compilation.

## Post-Installation Verification
### Setting Environment Variables
After installation, set environment variables to add the cross-compiler's location to the system's PATH.
This allows direct calling of the cross-compiler from any terminal location.
```bash
echo 'export PATH=/usr/cross/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```
Now, you can verify the installation of the cross-compiler, and use examples of Binutils tools like `ld` and `objcopy` to confirm the completion of the installation.

### GCC
The basis GCC compiles code for the system's native architecture, whereas the cross-compiler uses a target architecture specified, such as `x86_64-pc-linux-gnu-gcc`.
```bash
# gcc version
gcc -v

# Cross-compiler version
x86_64-pc-linux-gnu-gcc -v
```

### ld(Linker) / objcopy
```bash
# ld version
ld -v

# objcopy version
objcopy --version

# ld usage example
# This command links object files into an executable in the cross-compilation environment.
x86_64-pc-linux-gnu-ld -o output_file input_file.o

# objcopy usage example
# This command converts an executable file into another format (e.g., binary) in the cross-compilation environment.
x86_64-pc-linux-gnu-objcopy -O binary input_executable output_binary
```

This guide provides a basic outline for setting up a cross-compilation environment in Ubuntu, detailing the installation and usage of GCC and Binutils.
It includes version checks and functionality tests for the tools post-installation.
This guide should enable software development targeting various architectures.