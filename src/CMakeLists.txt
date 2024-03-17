set(PROJECT_NAME main_target)

set(VERSION_FILE_NAME version.txt)

# get versions from file
file (READ ${VERSION_FILE_NAME} FILE_VERSION)
string(REGEX MATCH "MAJOR ([0-9]*)" _ ${FILE_VERSION})
set(APP_MAJOR_VERSION ${CMAKE_MATCH_1})
string(REGEX MATCH "MINOR ([0-9]*)" _ ${FILE_VERSION})
set(APP_MINOR_VERSION ${CMAKE_MATCH_1})
string(REGEX MATCH "PATCH ([0-9]*)" _ ${FILE_VERSION})
set(APP_PATCH_VERSION ${CMAKE_MATCH_1})

if (NOT ${UPDATE_VERSION} STREQUAL "")
    message("Update Version...")
    if (${UPDATE_VERSION} STREQUAL "MAJOR")
        MATH(EXPR APP_MAJOR_VERSION "${APP_MAJOR_VERSION}+1")
    elseif (${UPDATE_VERSION} STREQUAL "MINOR")
        MATH(EXPR APP_MINOR_VERSION "${APP_MINOR_VERSION}+1")
    elseif (${UPDATE_VERSION} STREQUAL "PATCH")
        message("HERE")
        MATH(EXPR APP_PATCH_VERSION "${APP_PATCH_VERSION}+1")
    else()
        message (FATAL_ERROR "${UPDATE_VERSION} is an unknown option")
    endif()

    file(WRITE ${VERSION_FILE_NAME} "MAJOR ${APP_MAJOR_VERSION}\nMINOR ${APP_MINOR_VERSION}\nPATCH ${APP_PATCH_VERSION}")
    message("Version Updated")
endif()

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
