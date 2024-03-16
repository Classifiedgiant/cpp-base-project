set(PROJECT_NAME main_target)


project(${PROJECT_NAME})

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
