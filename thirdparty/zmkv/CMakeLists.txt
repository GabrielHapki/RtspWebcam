include(ExternalProject)
ExternalProject_Add(zmkv
    PREFIX zmkv
    # --- Download step ---
    URL                 ${CMAKE_CURRENT_SOURCE_DIR}/libzmkv.tar.bz2
    URL_MD5             93f04aa10ede48c894c844dc04c4d1a7
    # GIT_REPOSITORY      https://github.com/voximplant/zmkv.git
    # GIT_REMOTE_NAME     master
    CMAKE_ARGS          -DCMAKE_PREFIX_PATH=${CMAKE_INSTALL_OUTPUT_DIRECTORY}
                        -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_OUTPUT_DIRECTORY}
    # CMAKE_COMMAND       ${CMAKE_COMMAND}../zmkv
    UPDATE_COMMAND      ""
    INSTALL_COMMAND     ""
    LOG_DOWNLOAD        1
    LOG_CONFIGURE       1
    LOG_BUILD           1
    LOG_INSTALL         1
)

# ExternalProject_Get_Property(zmkv INSTALL_DIR)
# add_library(zmkv STATIC IMPORTED ${SOURCE_DIR})
# set_target_properties(zmkv PROPERTIES IMPORTED_LOCATION ${SOURCE_DIR}/liveMedia/libliveMedia.a)

set(ZMKV_INCLUDE_DIRS ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/include CACHE PATH "zmkv header directory" FORCE)
message(STATUS "zmkv Include directory: ${ZMKV_INCLUDE_DIRS}")

set(ZMKV_LIBRARIES ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/lib CACHE PATH "zmkv library directory" FORCE)
message(STATUS "zmkv Library directory: ${ZMKV_LIBRARIES}")

add_dependencies(zmkv matroska)