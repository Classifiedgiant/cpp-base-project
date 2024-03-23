set(PROJECT_NAME main_target)

set(VERSION_FILE_NAME version.txt)

# get versions from file
file (READ ${VERSION_FILE_NAME} FILE_VERSION)
string(REGEX MATCH "v([0-9]+)\.([0-9]+).([0-9]+)" _ ${FILE_VERSION})
set(APP_MAJOR_VERSION ${CMAKE_MATCH_1})
set(APP_MINOR_VERSION ${CMAKE_MATCH_2})
set(APP_PATCH_VERSION ${CMAKE_MATCH_3})

project(${PROJECT_NAME} VERSION ${APP_MAJOR_VERSION}.${APP_MINOR_VERSION}.${APP_PATCH_VERSION} LANGUAGES CXX)

message ("Version ${main_target_VERSION}")

add_executable(${PROJECT_NAME} main.cpp)

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION .)


# Cpack
# generic settings
set(CPACK_PACKAGE_NAME ${PROJECT_NAME})
set(CPACK_RESOURCE_FILE_LICENSE ${CMAKE_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README ${CMAKE_SOURCE_DIR}/README.md)

if(WIN32)

    set(CPACK_GENERATOR "ZIP")  # Specify the generator to create a ZIP package

elseif(APPLE)

    message("Apple builds not implemented yet!")

elseif (CMAKE_SYSTEM_NAME STREQUAL "Linux")

    message("Apple builds not implemented yet!")
endif()

include(CPack)
