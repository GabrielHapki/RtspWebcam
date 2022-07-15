include(ExternalProject)
ExternalProject_Add(loguru
    PREFIX loguru
    # --- Download step ---
    #URL                 http://download.videolan.org/pub/x264/snapshots/x264-snapshot-20191217-2245.tar.bz2
    URL                 ${CMAKE_CURRENT_SOURCE_DIR}/loguru-f64f3fc088392869142c7b170dbb015c2f79bd5a.tar.gz
    URL_MD5             81b6737e271d86dab9f2870bd8955370
    LOG_DOWNLOAD        1
    # --- Patch step ---
    PATCH_COMMAND       patch -p1 < ${CMAKE_CURRENT_SOURCE_DIR}/patch/0001-buildroot-makefile.patch
    COMMAND             patch -p1 < ${CMAKE_CURRENT_SOURCE_DIR}/patch/0002-fix-build-warning.patch
    #LOG_PATCH           1
    # --- Configure step ---
    CONFIGURE_COMMAND   ""
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

# ExternalProject_Add_Step(loguru copying
#     DEPENDEES           build
#     COMMAND             file(COPY ${SOURCE_DIR}/libloguru.so DESTINATION ${RUNTIME_PATH})
#     WORKING_DIRECTORY   ${SOURCE_DIR}
#     LOG                 1
# )

ExternalProject_Get_Property(loguru SOURCE_DIR)
# add_library(loguru STATIC IMPORTED)
# set_target_properties(loguru PROPERTIES IMPORTED_LOCATION ${SOURCE_DIR}/libx264.a)

set(LOGURU_INCLUDE_DIRS ${SOURCE_DIR} CACHE PATH "loguru header directory" FORCE)
message(STATUS "loguru Include directory: ${LOGURU_INCLUDE_DIRS}")

set(LOGURU_LIBRARIES ${SOURCE_DIR} CACHE PATH "loguru library directory" FORCE)
message(STATUS "loguru Library directory: ${LOGURU_LIBRARIES}")
