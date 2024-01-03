# Windows_Servercore_Rust_MSYS2 Dockerfile

This is a Dockerfile for creating windows servercore (ltsc 2019) as a base image with rust (GNU) and MSYS2 (GNU toolchain).
Image avaliable on dockerhub as : `docker pull ayush1822/win_servercore_ltsc-2019-gnu_rust-msys2`

### Windows Servercore image used

Image used : `mcr.microsoft.com/windows/servercore:ltsc2019`

Microsoft Artifacts Webpage: [Windows Server core](https://mcr.microsoft.com/en-us/product/windows/servercore/about)

Docker webpage: [Windows Server Core](https://hub.docker.com/_/microsoft-windows-servercore)

### Rust

Rust is installed with the help of this template on github: [docker-rust](https://github.com/yodaldevoid/docker-rust/blob/windows/Dockerfile-windows-gnu.template)

default-toolchain =   stable-x86_64-pc-windows-gnu
default-host      =   x86_64-pc-windows-gnu

### MSYS2

MSYS2 is installed using official MSYS-CI docs: [MSYS2 in Docker](https://www.msys2.org/docs/ci/#:~:text=Install%20MSYS2%20under%20C%3A%5Cmsys64%20into%20a%20Windows%20based%20Docker%20image%3A)

Install Packages   =    mingw-w64-x86_64-toolchain (all packages by default)
Install GCC        =    mingw-w64-x86_64-gcc
Install CMake      =    mingw-w64-x86_64-cmake

### Git

The servercore image supplied by Microsoft doesn't ship with git by default. So, it has to be installed by self.

The git is installed using this comment on Stack Overflow: [install git using powershell](https://stackoverflow.com/a/59210681)