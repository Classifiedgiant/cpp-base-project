![Main Branch](https://github.com/Classifiedgiant/cpp-base-project/actions/workflows/cmake-multi-platform-build-and-test.yml/badge.svg)
![Main Branch](https://github.com/Classifiedgiant/cpp-base-project/actions/workflows/bump-version.yml/badge.svg)
![Main Branch](https://github.com/Classifiedgiant/cpp-base-project/actions/workflows/create-release.yml/badge.svg)



# cpp-base-project

Base project for cpp projects. This project uses [conan](https://conan.io/center) for it dependency packages and provides customisable build pipelines from within the `.conan` folder.

CMakeLists files have been provided for the basic framework to quickly begin building applications rather than project setup. [Catch2](https://github.com/catchorg/Catch2) has been already added as a dependency and integreated to run tests when builds occur and is ready to begin usage.

[Github Actions](https://github.com/features/actions) have already been provided for CI/CD basics and test build on varying platforms. A manual tagging release github actions has also been provided to allow for packaging of your cpp application for various platforms (Though packaging and storage of these packages is yet to be implemented)

I have also included my personal .vscode settings for users that require them. Please feel free to delete the if you have no need for them.

`.clang-format` and `.clang-tidy` files have been provided for easy integration. `.clang-tidy` has had all reasonable checks turned on. Please Note `.clang-tidy` has been moved to the `src` folder as clang-tidy was very noisy interacting with `Catch2` in the test folder.

## Prerequisites

* Install Visual Studio (for Windows MSVC) or GCC on Linux
* Install CMake on your machine (Add to PATH)
* Install Python for Conan

## Setup Conan for building
* `conan install . -pr .\.conan\window_msvc_debug --build=missing` -- Pull deps from conan
   * `-pr .\.conan\window_msvc_debug` - Select profile to use for building
   * `--build=missing` - build missing
`cmake --preset --conan-default`
`cmake --preset conan-release` -- mac
`cmake --build --preset --conan-debug`


## Packing steps (Release only)
### Window
* conan install (as above with release profile)
* `cmake --preset conan-default`
   * Can be appended with `-DCMAKE_CONFIGURATION_TYPES=Debug` for Windows VS debug builds
* `cmake --build --preset conan-release`
* `cpack --config .\build\CPackConfig.cmake`
