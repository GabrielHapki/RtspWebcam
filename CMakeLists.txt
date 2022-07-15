cmake_minimum_required(VERSION 3.14.7)

get_filename_component(RUNTIME_PATH  . ABSOLUTE)
message(STATUS "Runtime path is " ${RUNTIME_PATH})

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread -rdynamic -Wall")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_INSTALL_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/install)

# Thirdparty libraries
add_subdirectory(thirdparty)

#add_subdirectory(libs)

add_subdirectory(apps)

# add_dependencies(${PROJECT_NAME} loguru)
# add_dependencies(${PROJECT_NAME} x264)
# add_dependencies(${PROJECT_NAME} live555)
# add_dependencies(${PROJECT_NAME} ebml)
# add_dependencies(${PROJECT_NAME} matroska)
