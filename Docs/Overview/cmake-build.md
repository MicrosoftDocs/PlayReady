---
title: PlayReady CMake Build Instructions
description: PlayReady Device Porting Kit Users can use CMake for building starting in PlayReady Device Porting Kit version 4.8.92.
ms.assetid: "4B900FF1-B839-4E8B-B8E4-97AE80D24219"
keywords: PlayReady build, cmake, PlayReady cmake
ms.date: 04/29/2026
ms.topic: article
---

# Building with CMake

## Toolchain

CMake builds require a **toolchain file** that configures compiler flags for the target platform.
Toolchain files are located in `<PK location>/cmake/toolchain/`

### Available Toolchain Files

| Toolchain File | Target |
|---|---|
| `windows-msvc.cmake` | Windows native (MSVC) |
| `linux-gcc-x86_64.cmake` | Linux x86_64 (GCC) |
| `linux-gcc-aarch64.cmake` | Linux aarch64 cross-compile (GCC) |
| `linux-clang-x86_64.cmake` | Linux x86_64 (Clang) |
| `linux-clang-aarch64.cmake` | Linux aarch64 cross-compile (Clang) |
| `macos-appleclang-arm64.cmake` | macOS ARM64 / Apple Silicon (AppleClang) |
| `macos-appleclang-x86_64.cmake` | macOS x86_64 / Intel (AppleClang) |

Each toolchain file includes a compiler flags module from `cmake/toolchain/flags/` (`msvc.cmake`, `gcc.cmake`, `clang.cmake`, `appleclang.cmake`).
To create a custom toolchain, include the appropriate flags module:

```cmake
# Example: my-custom-toolchain.cmake
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR x86_64)
set(CMAKE_C_COMPILER /path/to/my/gcc)
include(<PK location>/cmake/toolchain/flags/gcc.cmake)
```

## Build Steps

### Windows

**Starting Commands**
```powershell
$env:PK_BUILD_DIRECTORY="<Output path>"
$env:PK_GEN_DIRECTORY="<PK location>"
$env:WORKING_DIR="<Working Directory for cmake_install files>
```

**Powershell**
```powershell
cd $env:PK_GEN_DIRECTORY
cmake -DCMAKE_TOOLCHAIN_FILE="$env:PK_GEN_DIRECTORY\cmake\toolchain\windows-msvc.cmake" `
      -DCMAKE_INSTALL_PREFIX="$env:WORKING_DIR\cmake_install" `
      -DDRM_BUILD_PROFILE="OEM" `
      -S . -B $env:PK_BUILD_DIRECTORY

cmake --build $env:PK_BUILD_DIRECTORY [--config Debug/Release]

cmake --install $env:PK_BUILD_DIRECTORY [--config Debug/Release]
```

**PowerShell (Windows ARM64 cross-compile):**

To build ARM64 binaries on Windows, pass `-A ARM64` to select the ARM64 generator platform.

Note that this requires the **MSVC ARM64 build tools** to be installed in Visual Studio
(VS Installer > Individual components > search "ARM64").

```powershell
cmake -DCMAKE_TOOLCHAIN_FILE="$env:PK_GEN_DIRECTORY\cmake\toolchain\windows-msvc.cmake" `
      -DCMAKE_INSTALL_PREFIX="$env:WORKING_DIR\cmake_install" `
      -DDRM_BUILD_PROFILE="OEM" `
      -A ARM64 `
      -S . -B $env:PK_BUILD_DIRECTORY

cmake --build $env:PK_BUILD_DIRECTORY [--config Debug/Release]
```

### Linux / MacOS

**Bash**

Linux native build prerequisites:
```bash
sudo apt update
sudo apt install cmake build-essential libcurl4-openssl-dev libssl-dev zlib1g-dev
```

Linux aarch64 cross-compile prerequisites (on x86_64 host):

1. Add the arm64 architecture and the ports repository:
```bash
sudo dpkg --add-architecture arm64
```

1. Restrict existing apt sources to amd64 only. Edit `/etc/apt/sources.list.d/ubuntu.sources`
   and add `Architectures: amd64` before each `Types: deb` line:
```
Architectures: amd64
Types: deb
URIs: http://archive.ubuntu.com/ubuntu/
...
```

3. Add the arm64 ports repository. Create `/etc/apt/sources.list.d/arm64-ports.sources`
   with the following content (no leading spaces):
```
Types: deb
Architectures: arm64
URIs: http://ports.ubuntu.com/ubuntu-ports/
Suites: noble noble-updates
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
Architectures: arm64
URIs: http://ports.ubuntu.com/ubuntu-ports/
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

4. Install cross-compile toolchain and arm64 libraries:
```bash
sudo apt update
# For GCC cross-compilation:
sudo apt install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu binutils-aarch64-linux-gnu
# For Clang cross-compilation:
sudo apt install clang lld llvm libc6-dev-arm64-cross libstdc++-dev-arm64-cross
# arm64 libraries:
sudo apt install libcurl4-openssl-dev:arm64 libssl-dev:arm64 zlib1g-dev:arm64
```

5. Perform the CMake build:
```bash
# Set the toolchain file (pick one from the table above).
# Option A: pass it on the cmake command line (shown below)
# Option B: set it as an environment variable
#   export CMAKE_TOOLCHAIN_FILE=<PK location>/cmake/toolchain/<toolchain>.cmake

# Build and install PK
cd <PK location>
cmake -DCMAKE_TOOLCHAIN_FILE="<PK location>/cmake/toolchain/<toolchain>.cmake" \
      -DCMAKE_INSTALL_PREFIX="<Working Directory>/cmake_install" \
      -DDRM_BUILD_PROFILE="LINUX" \
      -S . -B <PK build directory>

cmake --build <PK build directory> [-c Debug/Release]

cmake --install <PK build directory> [-c Debug/Release]
```
