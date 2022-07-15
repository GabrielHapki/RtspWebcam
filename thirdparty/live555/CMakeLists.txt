include(ExternalProject)
ExternalProject_Add(live555
    PREFIX live555
    # --- Download step ---
    URL                 ${CMAKE_CURRENT_SOURCE_DIR}/live555.tar.bz2
    URL_MD5             4e0e01e19f4fe8f0dafbf20b494655ea
    # GIT_REPOSITORY      https://github.com/rgaufman/live555.git
    # GIT_REMOTE_NAME     master
    LOG_DOWNLOAD        1
    # --- Patch step ---
    PATCH_COMMAND       ""
    #LOG_PATCH           1
    # --- Configure step ---
    CONFIGURE_COMMAND   <SOURCE_DIR>/genMakefiles "linux"
    #LOG_CONFIGURE       1
    # --- Build step ---
    BUILD_IN_SOURCE     1
    #BUILT_ALWAYS        1
    BUILD_COMMAND       make -j${NCPU}
    LOG_BUILD           1
    # --- Install step ---
    UPDATE_COMMAND      ""
    INSTALL_COMMAND     ""
    # --- Test step ---
    TEST_COMMAND        ""
)

ExternalProject_Get_Property(live555 SOURCE_DIR)
# add_library(live555 STATIC IMPORTED ${SOURCE_DIR})
# set_target_properties(live555 PROPERTIES IMPORTED_LOCATION ${SOURCE_DIR}/liveMedia/libliveMedia.a)

set(LIVE555_INCLUDE_DIRS ${SOURCE_DIR}/liveMedia/include; ${SOURCE_DIR}/BasicUsageEnvironment/include; ${SOURCE_DIR}/UsageEnvironment/include; ${SOURCE_DIR}/groupsock/include; CACHE PATH "live555 header directory" FORCE)
message(STATUS "live555 Include directory: ${LIVE555_INCLUDE_DIRS}")

set(LIVE555_LIBRARIES ${SOURCE_DIR}/liveMedia; ${SOURCE_DIR}/BasicUsageEnvironment; ${SOURCE_DIR}/UsageEnvironment; ${SOURCE_DIR}/groupsock; CACHE PATH "live555 library directory" FORCE)
message(STATUS "live555 Library directory: ${LIVE555_LIBRARIES}")
