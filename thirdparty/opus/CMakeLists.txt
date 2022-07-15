include(ExternalProject)
ExternalProject_Add(opus
    PREFIX opus

    # --- Download step ---
    # URL                 ${CMAKE_CURRENT_SOURCE_DIR}/opus.tar.bz2
    # URL_MD5             a06e75a61ce2d5f0e3642be582abe738
    GIT_REPOSITORY      https://github.com/xiph/opus.git
    GIT_TAG             1.1.2
    LOG_DOWNLOAD        1

    # --- Patch step ---
    PATCH_COMMAND       ""
    #LOG_PATCH           1

    # --- Configure step ---
    CONFIGURE_COMMAND   <SOURCE_DIR>/autogen.sh
        COMMAND         <SOURCE_DIR>/configure --enable-static --enable-shared --prefix=${CMAKE_INSTALL_OUTPUT_DIRECTORY}
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

set(OPUS_INCLUDE_DIRS ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/include CACHE PATH "opus header directory" FORCE)
message(STATUS "opus Include directory: ${OPUS_INCLUDE_DIRS}")

set(OPUS_LIBRARIES ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/lib CACHE PATH "opus library directory" FORCE)
message(STATUS "opus Library directory: ${OPUS_LIBRARIES}")
