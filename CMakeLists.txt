cmake_minimum_required(VERSION 3.0)
project(simple_image_library)
if(UNIX)
    add_definitions(-std=c++17)
endif(UNIX)

include_directories(
	${CMAKE_SOURCE_DIR}/image 
	${CMAKE_SOURCE_DIR}/color 
	${CMAKE_SOURCE_DIR}/algorithms 
	${CMAKE_SOURCE_DIR}/adapters
	${CMAKE_SOURCE_DIR}/test)
	
aux_source_directory(${CMAKE_SOURCE_DIR} SRC_FILES)
aux_source_directory(${CMAKE_SOURCE_DIR}/image SRC_FILES)
aux_source_directory(${CMAKE_SOURCE_DIR}/algorithms SRC_FILES)
aux_source_directory(${CMAKE_SOURCE_DIR}/adapters SRC_FILES)
aux_source_directory(${CMAKE_SOURCE_DIR}/color SRC_FILES)
aux_source_directory(${CMAKE_SOURCE_DIR}/test SRC_FILES)

file (GLOB HEADER_FILES ${HEADER_FILES} "${CMAKE_SOURCE_DIR}/*.hpp")
file (GLOB HEADER_FILES ${HEADER_FILES} "${CMAKE_SOURCE_DIR}/algorithms/*.hpp")
file (GLOB HEADER_FILES ${HEADER_FILES} "${CMAKE_SOURCE_DIR}/adapters/*.hpp")
file (GLOB HEADER_FILES ${HEADER_FILES} "${CMAKE_SOURCE_DIR}/image/*.hpp")
file (GLOB HEADER_FILES ${HEADER_FILES} "${CMAKE_SOURCE_DIR}/color/*.hpp")
file (GLOB HEADER_FILES ${HEADER_FILES} "${CMAKE_SOURCE_DIR}/test/*.hpp")
	
find_package(JPEG REQUIRED)
if(JPEG_FOUND)
	set(LINK_LIBS ${LINK_LIBS} ${JPEG_LIBRARIES})
	include_directories(${JPEG_INCLUDE_DIR})   
endif(JPEG_FOUND)

add_executable(test_project ${SRC_FILES} ${HEADER_FILES})
target_link_libraries(test_project ${LINK_LIBS})