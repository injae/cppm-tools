cmake_minimum_required(VERSION 3.12)
project(cppm-tools VERSION 0.0.13 LANGUAGES NONE)

if(NOT CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    set(_IS_CPPM_TOOLS_TOP_LEVEL ON)
else()
    set(_IS_CPPM_TOOLS_TOP_LEVEL OFF)
endif()

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

include(GNUInstallDirs)

add_custom_target(cppm-tools)

include(CMakePackageConfigHelpers)

configure_package_config_file(
    ${PROJECT_NAME}-config.cmake.in ${PROJECT_NAME}-config.cmake
    INSTALL_DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}
)

set(CPPM_TOOLS_INSTALL_DESTINATION lib/cmake/${PROJECT_NAME})

#-- version file setting
write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
    VERSION ${${PROJECT_NAME}_VERSION}
    COMPATIBILITY SameMinorVersion # 0.2 != 0.3, 0.2 == 0.2.5
) 

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config-version.cmake
    DESTINATION ${CPPM_TOOLS_INSTALL_DESTINATION}
)

#-- cmake package file export
install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}-config.cmake
    DESTINATION ${CPPM_TOOLS_INSTALL_DESTINATION}
)

install(FILES cmake/core_load.cmake ${CPPM_TOOLS_INSTALL_DESTINATION})
