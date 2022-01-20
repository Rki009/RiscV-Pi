# RiscV Pi - RiscV for the Raspberry Pi

## Introduction
The Raspberry Pi 4 is a fast multi-core Linux systems. It can easily support the gcc RiscV development tools
and provide an effective platform for embedded RiscV development.

Recommended platform:
    Raspberry Pi 4
    4G byte or more of DDRAM memory
    32G or more disk space

## Build a Compiler
The RiscV gcc compiler tools can be built and installed from the "github.com/riscv" sources. This will build and install the latest version of tools. Note that it will take a long time to download, build and install the tools. About 6G bytes of space is needed for the build.
```
Install tools used to build Gcc:
    sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev
    sudo apt-get install gawk build-essential bison flex texinfo gperf libtool patchutils
    sudo apt-get install bc zlib1g-dev libexpat-dev

Remove any previous build:
    sudo rm -fr /opt/riscv
    sudo rm -fr ./riscv-gnu-toolchain

Clone the gcc build source tree:
    git clone --recursive https://github.com/riscv/riscv-gnu-toolchain

Configure the RiscV tool chain:
    cd riscv-gnu-toolchain
    ./configure --prefix=/opt/riscv

Make the tools:
    sudo make           -- for ELF tools
    sudo make linux     -- for Linux tools
```

## Using the Tools
The RiscV gcc compile will be installed into /opt/riscv.
```
Test the ELF compile, Target: riscv64-unknown-elf:
	/opt/riscv/bin/riscv64-unknown-elf-gcc -v

Test the Linux compile, Target: riscv64-unknown-linux-gnu:
	/opt/riscv/bin/riscv64-unknown-linux-gnu-gcc -v

```

## Links
Some useful links ...

### Riscv.org:
https://riscv.org/technical/specifications/

### Unprivileged Spec:
https://github.com/riscv/riscv-isa-manual/releases/download/Ratified-IMAFDQC/riscv-spec-20191213.pdf

### Privileged Spec:
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
