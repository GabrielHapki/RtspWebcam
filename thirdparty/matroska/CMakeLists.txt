message(STATUS "EBML_INSTALL_DIR: ${EBML_INSTALL_DIR}")

include(ExternalProject)
ExternalProject_Add(matroska
    PREFIX matroska
    URL                 ${CMAKE_CURRENT_SOURCE_DIR}/libmatroska.tar.bz2
    URL_MD5             ddb291d394c1c4dd2bdd4bb1f8156b1e
    # GIT_REPOSITORY      https://github.com/Matroska-Org/libmatroska.git
    # GIT_REMOTE_NAME     master
    CMAKE_ARGS          -DCMAKE_PREFIX_PATH=${CMAKE_INSTALL_OUTPUT_DIRECTORY}
                        -DBUILD_SHARED_LIBS=YES
                        -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_OUTPUT_DIRECTORY}
    UPDATE_COMMAND      ""
    LOG_DOWNLOAD        1
    LOG_CONFIGURE       1
    LOG_BUILD           1
    LOG_INSTALL         1
)

# ExternalProject_Get_Property(matroska INSTALL_DIR)
# add_library(matroska STATIC IMPORTED ${SOURCE_DIR})
# set_target_properties(matroska PROPERTIES IMPORTED_LOCATION ${SOURCE_DIR}/liveMedia/libliveMedia.a)

set(MATROSKA_INCLUDE_DIRS ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/include CACHE PATH "matroska header directory" FORCE)
message(STATUS "matroska Include directory: ${MATROSKA_INCLUDE_DIRS}")

set(MATROSKA_LIBRARIES ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/lib CACHE PATH "matroska library directory" FORCE)
message(STATUS "matroska Library directory: ${MATROSKA_LIBRARIES}")

add_dependencies(matroska ebml)
