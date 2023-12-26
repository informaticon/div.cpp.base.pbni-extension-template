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

add_library(°°°PACKAGE_NAME°°° SHARED
	# Add your source files here
	# Example: src/main.cpp
	°°°SOURCE_FILES°°°
)


target_compile_features(°°°PACKAGE_NAME°°° PUBLIC cxx_std_20)

set_target_properties(°°°PACKAGE_NAME°°°
PROPERTIES
	OUTPUT_NAME "${CMAKE_PROJECT_NAME}"
	RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_PATH}
 	# Because vcpkg x86-windows-static sets this in dependencies, but not the main project
 	MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>"

)

string(TIMESTAMP BUILD_NR "%Y,%m,%d,%H%M")
target_compile_definitions(°°°PACKAGE_NAME°°°
PUBLIC
	VER_BUILD_NR=${BUILD_NR}
	VER_COMPANY_STR="Informaticon AG"
	VER_NAME_STR="${PROJECT_NAME}"
	VER_VERSION_STR="${VERSION_STR}"
)
target_sources(°°°PACKAGE_NAME°°° PRIVATE res/version.rc)

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
