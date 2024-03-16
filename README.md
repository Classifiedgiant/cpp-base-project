# cpp-base-project

Base project for cpp projects

## Prerequisites

* Install Visual Studio (for Windows MSVC) or GCC on Linux
* Install CMake on your machine (Add to PATH)
* Install Python for Conan or Poetry
* (Windows Only) - Install Ninja for compile_commands generation

## Setup Conan for building
* `conan install . -pr .\.conan\window_msvc_debug --build=missing` -- Pull deps from conan
   * `-pr .\.conan\window_msvc_debug` - Select profile to use for building
   * `--build=missing` - build missing
`cmake --preset --conan-default`
`cmake --build --preset --conan-debug`


## Packing steps (Release only)
### Window
* conan install (as above with release profile)
* `cmake --preset conan-default`
   * Can be appended with `-DCMAKE_CONFIGURATION_TYPES=Debug` for Windows VS debug builds
* `cmake --build --preset conan-release`
* `cpack --config .\build\CPackConfig.cmake`
