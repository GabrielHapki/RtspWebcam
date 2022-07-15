project(webcam VERSION 0.0.0)

include_directories(
	includes
    ${LIVE555_INCLUDE_DIRS}
    ${X264_INCLUDE_DIRS}
)

link_directories(
    ${LIVE555_LIBRARIES}	
    ${X264_LIBRARIES}
)

add_executable(${PROJECT_NAME}
	src/H264LiveServerMediaSession.cpp
	src/LiveSourceWithx264.cpp
	src/x264Encoder.cpp
	src/webcam.cpp
)

#set(EXECUTABLE_OUTPUT_PATH  ../bin/)
target_link_libraries(${PROJECT_NAME} -lliveMedia -lBasicUsageEnvironment -lUsageEnvironment -lgroupsock -lx264 -lpthread -ldl)

add_dependencies(${PROJECT_NAME} x264)
add_dependencies(${PROJECT_NAME} live555)