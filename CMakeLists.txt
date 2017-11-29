cmake_minimum_required(VERSION 3.0)
project (Tiny_XML DESCRIPTION "Cmake for tinyxml as a hunter package")
set(CMAKE_BUILD_TYPE Release)


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


include_directories(Tiny_XML 
	PRIVATE src 
	PUBLIC "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>"
)

add_library(Tiny_XML SHARED
    ${Tiny_XML_Header_Files}
    ${Tiny_XML_SRC}
)




################Installation (https://github.com/forexample/package-example) {
set(config_install_dir "lib/cmake/${PROJECT_NAME}")
set(include_install_dir "include")

set(generated_dir "${CMAKE_CURRENT_BINARY_DIR}/generated")

set(version_config "${generated_dir}/${PROJECT_NAME}ConfigVersion.cmake")
set(project_config "${generated_dir}/${PROJECT_NAME}Config.cmake")
set(TARGETS_EXPORT_NAME "${PROJECT_NAME}Targets")
set(namespace "${PROJECT_NAME}::")
#####################

install(
    TARGETS Tiny_XML
    EXPORT "${TARGETS_EXPORT_NAME}"
    LIBRARY DESTINATION "lib"
    ARCHIVE DESTINATION "lib"
    RUNTIME DESTINATION "bin"
    INCLUDES DESTINATION "${include_install_dir}"
)