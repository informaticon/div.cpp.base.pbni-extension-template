cmake_minimum_required(VERSION 3.15)


##################################################
#                    Options                     #
##################################################

set(OUTPUT_PATH "${CMAKE_SOURCE_DIR}/out" CACHE PATH "Location of built dlls/libraries")
set(INSTALL_PATH "${CMAKE_SOURCE_DIR}/pbproj" CACHE PATH "Location where the resulting DLL shall be placed in")
set(VERSION_STR "0.0.0-trunk" CACHE STRING "Version number to add to the DLL")
set(COMPANY_NAME "" CACHE STRING "")

##################################################
#               °°°PACKAGE_NAME°°°               #
##################################################

project(°°°PACKAGE_NAME°°° LANGUAGES CXX)

add_library(${PROJECT_NAME} SHARED
	°°°SOURCE_NAME°°°
)

set_target_properties(${PROJECT_NAME}
PROPERTIES
	OUTPUT_NAME ${PROJECT_NAME}
	RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_PATH}
 	# Because vcpkg x86-windows-static sets this in dependencies, but not the main project
 	MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>"

)

string(TIMESTAMP BUILD_NR "%Y,%m,%d,%H%M")
target_compile_definitions(${PROJECT_NAME}
PUBLIC
	VER_BUILD_NR=${BUILD_NR}
	VER_COMPANY_STR="${COMPANY_NAME}"
	VER_NAME_STR="${PROJECT_NAME}"
	VER_VERSION_STR="${VERSION_STR}"
)
target_sources(${PROJECT_NAME} PRIVATE res/version.rc)

# Warning doesn't affect us, since we use a fixed Boost version
set(Boost_NO_WARN_NEW_VERSIONS "1")


find_package(pbni-framework CONFIG REQUIRED)
target_link_libraries(${PROJECT_NAME}
PRIVATE
	inf::pbni-framework
)

target_precompile_headers(${PROJECT_NAME} PUBLIC ${PBNI_FRAMEWORK_HEADERS})

if (NOT INSTALL_PATH STREQUAL "")
	install(TARGETS ${PROJECT_NAME}
		RUNTIME DESTINATION ${INSTALL_PATH}
	)
endif()
