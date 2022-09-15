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

set(CPACK_WIX_EXTRA_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/srcml_extra_dialog.wxs")

set(CPACK_WIX_PATCH_FILE "${CMAKE_CURRENT_SOURCE_DIR}/patch_path_env.xml")

set(CPACK_WIX_TEMPLATE "${CMAKE_CURRENT_SOURCE_DIR}/WIX.template.in")

include(InstallRequiredSystemLibraries)

# needs to be last so not overwritten
include(CPack)
