cmake_minimum_required(VERSION 3.24)

project(Greeting)

add_executable(Greeting Greeting.cpp)

install(TARGETS Greeting DESTINATION bin COMPONENT SRCML)

install(FILES blank.hpp DESTINATION include COMPONENT SRCML)

# Package name
set(CPACK_PACKAGE_NAME "Greeting")

set(CPACK_PACKAGE_FILE_NAME "Greeting-Win")
if(MSVC)
    set(CPACK_GENERATOR "WIX")
endif()

set(CPACK_WIX_PRODUCT_GUID "8EB65BD8-DF5B-4DED-A642-80BDBBDEB58C")

set(CPACK_WIX_UPGRADE_GUID "278604DF-BD50-410A-9475-993006D98663")

set(CPACK_WIX_UI_DIALOG "${CMAKE_CURRENT_SOURCE_DIR}/background.png")

set(CPACK_WIX_UI_REF "srcMLUI_InstallDir")

set(CPACK_WIX_CMAKE_PACKAGE_REGISTRY srcML)

# summary
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Greeting")

set(CPACK_STRIP_FILES ON)

# output directory
set(CPACK_PACKAGE_DIRECTORY ${CMAKE_BINARY_DIR}/dist)

# directory name
set(CPACK_PACKAGE_INSTALL_DIRECTORY "Greeting")

set(CPACK_WIX_EXTRA_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/srcml_extra_dialog.wxs" "${CMAKE_CURRENT_SOURCE_DIR}/install_dir.wxs")

set(CPACK_WIX_PATCH_FILE "${CMAKE_CURRENT_SOURCE_DIR}/patch_path_env.xml;${CMAKE_CURRENT_SOURCE_DIR}/patch_product.xml")

set(CPACK_WIX_TEMPLATE "${CMAKE_CURRENT_SOURCE_DIR}/WIX.template.in")

set(CMAKE_INSTALL_SYSTEM_RUNTIME_COMPONENT SRCML)

# add examples
file(GLOB EXAMPLES "examples/srcml_*.c")

message("EXAMPLES: ${EXAMPLES}")

# add one-by-one to avoid problems with long lists
foreach(EXAMPLE ${EXAMPLES})
    message("SETUP INSTALL FOR: ${EXAMPLE}")
    install(FILES "${EXAMPLE}" DESTINATION share/srcml/examples COMPONENT EXAMPLES)
endforeach()

include(InstallRequiredSystemLibraries)

# needs to be last so not overwritten
include(CPack)
