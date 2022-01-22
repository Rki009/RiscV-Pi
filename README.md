# RiscV Pi - RiscV for the Raspberry Pi

## Introduction
The Raspberry Pi 4 is a fast multi-core Linux systems. It can easily support the gcc RiscV development tools
and provide an effective platform for embedded RiscV development.

Recommended platform:
    Raspberry Pi 4
    4G byte or more of DDRAM memory
    32G or more disk space

## Building a RiscV gcc Compiler
The RiscV gcc compiler tools can be built and installed from the "github.com/riscv" sources. This will build and install the latest version of tools. Note that it will take a long time to download, build and install the tools. About 6G bytes of space is needed for the build.
Configure with "--enable-multilib" to build both rv64 and rv32 versions of the gcc tools.
Either ELF (Newlib) or Linux versions of the tools can be built with the "make" or "make Linux" command.
```
Install tools used to build Gcc:
    sudo apt-get install autoconf automake autotools-dev curl python3
    sudo apt-get install libmpc-dev libmpfr-dev libgmp-dev
    sudo apt-get install gawk build-essential bison flex texinfo gperf
    sudo apt-get install libtool patchutilsbc zlib1g-dev libexpat-dev

Remove any previous build:
    sudo rm -fr /opt/riscv
    sudo rm -fr ./riscv-gnu-toolchain

Clone the gcc build source tree:
    git clone --recursive https://github.com/riscv/riscv-gnu-toolchain

Configure the RiscV tool chain:
    cd riscv-gnu-toolchain
    ./configure --prefix=/opt/riscv --enable-multilib

Make the tools (-j4 - use all 4 Raspberry Pi cores):
    sudo make -j4           -- for ELF tools
    OR
    sudo make -j4 linux     -- for Linux tools
```
### Libraries built
```
ELF + --enable-multilib:
    rv32i, rv32iac, rv32im, rv32imac, rv32imafc, rv64imac
```

## Using the Tools
The RiscV gcc compile will be installed into /opt/riscv.
```
Test the ELF compile, Target: riscv64-unknown-elf:
    /opt/riscv/bin/riscv64-unknown-elf-gcc -v

Test the Linux compile, Target: riscv64-unknown-linux-gnu:
    /opt/riscv/bin/riscv64-unknown-linux-gnu-gcc -v
```
### Compiling with RiscV gcc
```
32bit Newlib ELF with rv32i only instructions:
    /opt/riscv/bin/riscv64-unknown-elf-gcc -O3 -march=rv32i -mabi=ilp32 Test.cpp -o Test32.elf
    /opt/riscv/bin/riscv64-unknown-elf-objdump -d -h Test32.elf >Test32.lst

64bit Newlib ELF with rv64id instructions:
    /opt/riscv/bin/riscv64-unknown-elf-gcc -O3 -march=rv64imac -mabi=lp64 -mtune=rocket -mcmodel=medlow Test.cpp -o Test64.elf
    /opt/riscv/bin/riscv64-unknown-elf-objdump -d -h Test64.elf >Test64.lst
```

### Add paths and shortcuts to .bashrc
```
Add to your .bashrc file:
    # RISC-V Compiler
    export RISCV=/opt/riscv
    export PATH=$PATH:$RISCV/bin
```
### What next
The RiscV gcc can be used to develop and compile C and C++ programs for the 32 bit and 64 bit RISC-V architecture. It can be used to support actual hardware, FGPA soft cores or used with a simulator.

The RiscV-Fast simulator can be used to run rv32im bare metal or Newlib programs at 140+ DMIPS on a Raspberry Pi 4. This is very fast for a simulated environment add allows real-time simulation of 100+ MHz embedded RISC-V hardware or FPGA soft core.

## Notes
It takes time ... Downloading the gcc repository from git depends on the speed of your internet connection. There is about 6GB of files so it will take a while. Building a RiscV gcc compiler takes about 2 hours on the Raspberry Pi 4 using all cores.

## RISC-V Links
Some useful links ...

### RISC-V
Wikipedia has a very good overview of the RISC-V architecture.

https://en.wikipedia.org/wiki/RISC-V

https://riscv.org/technical/specifications/

### Unprivileged Spec
https://github.com/riscv/riscv-isa-manual/releases/download/Ratified-IMAFDQC/riscv-spec-20191213.pdf

### Privileged Spec
https://github.com/riscv/riscv-isa-manual/releases/download/Priv-v1.12/riscv-privileged-20211203.pdf


## License

    Copyright (c) 2022 Ron K. Irvine
    
    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction for personal use only, including without
    limitation the rights to use, copy, modify, merge, publish and distribute
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:
    
    The Software may not be used in connection with any commercial purposes, except as
    specifically approved by Ron K. Irvine or his representative. Unauthorized usage of
    the Software or any part of the Software is prohibited. Appropriate legal action
    will be taken by us for any illegal or unauthorized use of the Software.
    
    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.
    
    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.
