cmake_minimum_required(VERSION 3.27)

# Set for IDE (VScode) purposes
set (CMAKE_EXPORT_COMPILE_COMMANDS ON)

set (CXX_STANDARD 23)

set (UPDATE_VERSION "" CACHE STRING "version update for project")

project(root)

add_subdirectory(src)
add_subdirectory(test)
