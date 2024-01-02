# escape=`

FROM mcr.microsoft.com/windows/servercore:ltsc2019
# Using WIndows Servercore image ltsc 2019

SHELL ["powershell.exe", "-NoLogo", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Seting up basic Environment variables
ENV RUSTUP_HOME=C:\rustup `
    CARGO_HOME=C:\cargo `
    RUST_BACKTRACE="full" `
    RUST_MIN_STACK=20971520 `
    CARGO_NET_GIT_FETCH_WITH_CLI="true" `
    MSYS_HOME=C:\msys64\mingw64


# Installing Rust
RUN [Net.ServicePointManager]::SecurityProtocol = [Net.ServicePointManager]::SecurityProtocol -bor [Net.SecurityProtocolType]::Tls12; `
    $url = 'https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-gnu/rustup-init.exe'; `
    Invoke-WebRequest -Uri $url -OutFile C:\rustup-init.exe; `
    New-Item ${env:CARGO_HOME}\bin -type directory | Out-Null; `
    $newPath = ('{0}\bin;{1}' -f ${env:CARGO_HOME}, ${env:PATH}); `
    [Environment]::SetEnvironmentVariable('PATH', $newPath, [EnvironmentVariableTarget]::Machine); `
    [Environment]::SetEnvironmentVariable('PATH', $newPath, [EnvironmentVariableTarget]::Process); `
    C:\rustup-init.exe -y -v --no-modify-path --default-toolchain stable-x86_64-pc-windows-gnu --default-host x86_64-pc-windows-gnu; `
    Remove-Item C:\rustup-init.exe; `
    rustup -V; `
    cargo -V; `
    rustc -V;


# Installing MSYS2 Toolchain
RUN [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; `
    $url = 'https://github.com/msys2/msys2-installer/releases/download/nightly-x86_64/msys2-base-x86_64-latest.sfx.exe'; `
    Invoke-WebRequest -UseBasicParsing -uri $url -OutFile msys2.exe; `
    New-Item ${env:MSYS_HOME}\bin -type directory | Out-Null; `
    $newPath = ('{0}\bin;{1}' -f ${env:MSYS_HOME}, ${env:PATH}); `
    [Environment]::SetEnvironmentVariable('PATH', $newPath, [EnvironmentVariableTarget]::Machine); `
    [Environment]::SetEnvironmentVariable('PATH', $newPath, [EnvironmentVariableTarget]::Process); `
    .\msys2.exe -y -oC:\; `
    Remove-Item msys2.exe ; `
    function msys() { C:\msys64\usr\bin\bash.exe @('-lc') + @Args; } `
    msys ' '; `
    msys 'pacman --noconfirm -Syuu'; `
    msys 'pacman --noconfirm -Syuu'; `
    msys 'pacman --noconfirm -Syu'; `
    msys 'pacman --noconfirm -Su '; `
    msys 'pacman --noconfirm -S mingw-w64-x86_64-toolchain'; `
    msys 'pacman --noconfirm -S mingw-w64-x86_64-gcc'; `
    msys 'pacman --noconfirm -S mingw-w64-x86_64-cmake';


#Installing git
RUN Invoke-WebRequest 'https://github.com/git-for-windows/git/releases/download/v2.12.2.windows.2/MinGit-2.12.2.2-64-bit.zip' -OutFile MinGit.zip; `
    Expand-Archive c:\MinGit.zip -DestinationPath c:\MinGit; `
    $newPath = $env:PATH + ';C:\MinGit\cmd\;C:\MinGit\cmd'; `
    [Environment]::SetEnvironmentVariable('PATH', $newPath, [EnvironmentVariableTarget]::Machine); `
    [Environment]::SetEnvironmentVariable('PATH', $newPath, [EnvironmentVariableTarget]::Process); `
    Remove-Item C:\MinGit.zip; `
    git --version;


# Checking Environment Variables
RUN $env:RUST_BACKTRACE; `
    $env:RUST_MIN_STACK; `
    $env:CARGO_NET_GIT_FETCH_WITH_CLI; `
    $Env:PATH;