cmake_minimum_required(VERSION 3.15)


##################################################
#                    Options                     #
##################################################

set(OUTPUT_PATH "${CMAKE_SOURCE_DIR}/out" CACHE PATH "Location of built dlls/libraries")
set(A3_LIB_PATH "" CACHE PATH "Location of A3, is used to copy the resulting DLL when running INSTALL")


##################################################
#                  templateLib                   #
##################################################

project(div.cpp.base.pbni-extension-template VERSION 0.0.1 LANGUAGES CXX)
 

add_library(templateLib SHARED
	# Add your source files here
	# Example: src/main.cpp
)


target_compile_features(templateLib PUBLIC cxx_std_20)

set_target_properties(templateLib
PROPERTIES
	OUTPUT_NAME lib.pbni.base.libcurl
	RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_PATH}
	LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_PATH}
)

if (NOT A3_LIB_PATH STREQUAL "")
	install(TARGETS templateLib
		RUNTIME DESTINATION ${A3_LIB_PATH}
	)
endif()

add_subdirectory(extern)
find_package(CURL REQUIRED)

target_link_libraries(templateLib
PRIVATE
	libPBNIFramework
)