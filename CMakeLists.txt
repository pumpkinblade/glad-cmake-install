cmake_minimum_required(VERSION 3.17)

project(glad)

add_library(glad src/glad.c)

target_include_directories(glad PRIVATE include)

target_include_directories(glad INTERFACE 
	$<INSTALL_INTERFACE:include>
)

message(STATUS "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>/include")

## New Install With Export Config
install(TARGETS glad
	EXPORT gladTargets
	DESTINATION lib
)
install(DIRECTORY include/KHR DESTINATION include)
install(DIRECTORY include/glad DESTINATION include)
install(EXPORT gladTargets
	NAMESPACE glad::
	FILE gladTargets.cmake
	DESTINATION lib/cmake/glad
)
include(CMakePackageConfigHelpers)
# generate the config file that include the exports
configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in
	${CMAKE_CURRENT_BINARY_DIR}/gladConfig.cmake
	INSTALL_DESTINATION "lib/cmake/glad"
	NO_SET_AND_CHECK_MACRO
	NO_CHECK_REQUIRED_COMPONENTS_MACRO
)
install(FILES
	${CMAKE_CURRENT_BINARY_DIR}/gladConfig.cmake
	DESTINATION lib/cmake/glad
)
export(EXPORT gladTargets
	FILE ${CMAKE_CURRENT_BINARY_DIR}/gladTargets.cmake
)
