cmake_minimum_required(VERSION 3.15)


##################################################
#                    Options                     #
##################################################

set(OUTPUT_PATH "${CMAKE_SOURCE_DIR}/out" CACHE PATH "Location of built dlls/libraries")
set(A3_LIB_PATH "" CACHE PATH "Location of A3, is used to copy the resulting DLL when running INSTALL")
set(VERSION_STR "" CACHE STRING "Version number to add to the DLL")

##################################################
#               °°°PACKAGE_NAME°°°               #
##################################################

project(°°°PACKAGE_NAME°°° LANGUAGES CXX)

string(TIMESTAMP BUILD_NR "%Y,%m,%d,%H%M")
add_definitions(-DVER_BUILD_NR=${BUILD_NR})
add_definitions(-DVER_COMPANY_STR="Informaticon AG")
add_definitions(-DVER_NAME_STR="${PROJECT_NAME}")
add_definitions(-DVER_VERSION_STR="${VERSION_STR}")

add_library(°°°PACKAGE_NAME°°° SHARED
	# Add your source files here
	# Example: src/main.cpp
	°°°SOURCE_FILES°°°
	src/version.rc
)

source_group("Source Files"
FILES
	# Add your source files here
	# Example: src/main.cpp
	°°°SOURCE_FILES°°°
)

target_compile_features(°°°PACKAGE_NAME°°° PUBLIC cxx_std_20)

set_target_properties(°°°PACKAGE_NAME°°°
PROPERTIES
	OUTPUT_NAME °°°PACKAGE_NAME°°°
	RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_PATH}
 	# Because vcpkg x86-windows-static sets this in dependencies, but not the main project
 	MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>"

)

# Warning doesn't affect us, since we use a fixed Boost version
set(Boost_NO_WARN_NEW_VERSIONS "1")

find_package(pbni-framework CONFIG REQUIRED)
target_link_libraries(°°°PACKAGE_NAME°°°
PRIVATE
	inf::pbni-framework
)


if (NOT A3_LIB_PATH STREQUAL "")
	install(TARGETS °°°PACKAGE_NAME°°°
		RUNTIME DESTINATION ${A3_LIB_PATH}
	)
endif()
