cmake_minimum_required(VERSION 3.24)

project(Greeting)

add_executable(Greeting Greeting.cpp)

install(TARGETS Greeting COMPONENT Greeting)

set(CPACK_COMPONENTS_GROUPING "ALL_COMPONENTS_IN_ONE")

# Package name
set(CPACK_PACKAGE_NAME "Greeting")

set(SRCML_PACKAGE_RELEASE 1)

# executables and text label
set(CPACK_PACKAGE_EXECUTABLES Greeting)

# desktop links
set(CPACK_CREATE_DESKTOP_LINKS "${CPACK_PACKAGE_NAME}")

set(CPACK_PACKAGE_FILE_NAME "Greeting")
if(MSVC)
    set(CPACK_GENERATOR "WIX")
endif()

# summary
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Greeting")

# description
# set(CPACK_PACKAGE_DESCRIPTION_FILE ${CMAKE_SOURCE_DIR}/package/welcome.html)

# vendor
set(CPACK_PACKAGE_VENDOR "Greeting")

# contact
set(CPACK_PACKAGE_CONTACT "Greeting")

set(CPACK_STRIP_FILES ON)

# output directory
set(CPACK_PACKAGE_DIRECTORY ${CMAKE_BINARY_DIR}/dist)

# Generate user and development tar.gz's
set(CPACK_ARCHIVE_COMPONENT_INSTALL ON)

# directory name
set(CPACK_PACKAGE_INSTALL_DIRECTORY "Greeting")

# set contact in add/remove programs
set(CPACK_NSIS_CONTACT "Greeting <srcML.org>")

# set(CPACK_WIX_EXTRA_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/srcml_extra_dialog.wxs")
# set(CPACK_WIX_PATCH_FILE "${CMAKE_CURRENT_SOURCE_DIR}/patch_path_env.xml")
# set(CPACK_WIX_TEMPLATE "${CMAKE_CURRENT_SOURCE_DIR}/WIX.template.in")

# needs to be last so not overwritten
include(CPack)

# Client component, SRCML, is just one component so it appears as on item
# for installers that let you pick what to install
# Development group, SRCMLDEV, is composed of multiple components
include(CPackComponent)
cpack_add_component(SRCML
                    DISPLAY_NAME "srcml"
                    DESCRIPTION "srcml cli program with required library"
                    REQUIRED)
