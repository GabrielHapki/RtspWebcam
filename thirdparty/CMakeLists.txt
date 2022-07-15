include(ProcessorCount)
ProcessorCount(NCPU)

add_subdirectory(x264)
add_subdirectory(live555)
#add_subdirectory(loguru)
#add_subdirectory(opus)
#add_subdirectory(ebml)
#add_subdirectory(matroska)
#add_subdirectory(zmkv)

#https://mirkokiefer.com/cmake-by-example-f95eb47d45b1

#https://stackoverflow.com/questions/40314785/linking-against-an-externalproject-add-dependency-in-cmake