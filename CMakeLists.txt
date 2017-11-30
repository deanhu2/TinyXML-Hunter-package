cmake_minimum_required(VERSION 3.0)
project(TinyXML VERSION 1.0.3)


SET(Tiny_XML_SRC
    ${CMAKE_CURRENT_SOURCE_DIR}/src/tinystr.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/tinyxml.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/tinyxmlerror.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/tinyxmlparser.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/src/xmltest.cpp
)


set(Tiny_XML_Header_Files
	${CMAKE_CURRENT_SOURCE_DIR}/src/tinystr.h
	${CMAKE_CURRENT_SOURCE_DIR}/src/tinyxml.h
)


add_library(TinyXML ${Tiny_XML_Header_Files} ${Tiny_XML_SRC})

target_include_directories(
    TinyXML
    PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>"
)

# Installation (https://github.com/forexample/package-example) {

set(config_install_dir "lib/cmake/${PROJECT_NAME}")
set(include_install_dir "include")

set(generated_dir "${CMAKE_CURRENT_BINARY_DIR}/generated")

set(version_config "${generated_dir}/${PROJECT_NAME}ConfigVersion.cmake")
set(project_config "${generated_dir}/${PROJECT_NAME}Config.cmake")
set(TARGETS_EXPORT_NAME "${PROJECT_NAME}Targets")
set(namespace "${PROJECT_NAME}::")

include(CMakePackageConfigHelpers)

# Use:
#   * PROJECT_VERSION
write_basic_package_version_file(
    "${version_config}" COMPATIBILITY SameMajorVersion
)

# Use:
#   * TARGETS_EXPORT_NAME
#   * PROJECT_NAME
configure_package_config_file(
    "cmake/Config.cmake.in"
    "${project_config}"
    INSTALL_DESTINATION "${config_install_dir}"
)

install(
    TARGETS TinyXML
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "lib"
    ARCHIVE DESTINATION "lib"
    RUNTIME DESTINATION "bin"
    INCLUDES DESTINATION "${include_install_dir}"
)


install(
    FILES "${project_config}" "${version_config}"
    DESTINATION "${config_install_dir}"
)

install(
    FILES ${Tiny_XML_Header_Files}
    DESTINATION "${include_install_dir}"
)

install(
    EXPORT "${TARGETS_EXPORT_NAME}"
    NAMESPACE "${namespace}"
    DESTINATION "${config_install_dir}"
)




