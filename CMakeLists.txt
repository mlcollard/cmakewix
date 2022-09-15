cmake_minimum_required(VERSION 3.24)

project(Greeting)

add_executable(Greeting Greeting.cpp)

install(TARGETS Greeting DESTINATION bin)

# Package name
set(CPACK_PACKAGE_NAME "Greeting")

set(CPACK_PACKAGE_FILE_NAME "Greeting-Win")
if(MSVC)
    set(CPACK_GENERATOR "WIX")
endif()

# summary
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Greeting")

set(CPACK_STRIP_FILES ON)

# output directory
set(CPACK_PACKAGE_DIRECTORY ${CMAKE_BINARY_DIR}/dist)

# directory name
set(CPACK_PACKAGE_INSTALL_DIRECTORY "Greeting")

# needs to be last so not overwritten
include(CPack)
