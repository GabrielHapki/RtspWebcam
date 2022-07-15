include(ExternalProject)
ExternalProject_Add(x264
    PREFIX x264

    # --- Download step ---
    URL                 ${CMAKE_CURRENT_SOURCE_DIR}/x264-snapshot-20191217-2245.tar.bz2
    URL_MD5             6d6b7b49518ddfd42c4e3577b5242b31
    #URL                 http://download.videolan.org/pub/x264/snapshots/x264-snapshot-20191217-2245.tar.bz2
    LOG_DOWNLOAD        1

    # --- Patch step ---
    PATCH_COMMAND       ""
    #LOG_PATCH           1

    # --- Configure step ---
    CONFIGURE_COMMAND   <SOURCE_DIR>/configure --bindir="bin" --enable-static --enable-shared --disable-asm --prefix=${CMAKE_INSTALL_OUTPUT_DIRECTORY}
    #LOG_CONFIGURE       1

    # --- Build step ---
    BUILD_IN_SOURCE     1
    #BUILT_ALWAYS        1
    BUILD_COMMAND       make -j${NCPU}
    LOG_BUILD           1

    # --- Install step ---
    UPDATE_COMMAND      ""
    INSTALL_COMMAND     make install

    # --- Test step ---
    TEST_COMMAND        ""
)

# ExternalProject_Get_Property(x264 SOURCE_DIR)
# add_library(x264 STATIC IMPORTED)
# set_target_properties(x264 PROPERTIES IMPORTED_LOCATION ${SOURCE_DIR}/libx264.a)

set(X264_INCLUDE_DIRS ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/include CACHE PATH "x264 header directory" FORCE)
message(STATUS "x264 Include directory: ${X264_INCLUDE_DIRS}")

set(X264_LIBRARIES ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/lib CACHE PATH "X264 library directory" FORCE)
message(STATUS "x264 Library directory: ${X264_LIBRARIES}")
