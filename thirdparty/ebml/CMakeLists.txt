#find_program(MAKE_EXECUTABLE NAMES gmake make mingw32-make)

include(ExternalProject)
ExternalProject_Add(ebml
    PREFIX ebml
    URL                 ${CMAKE_CURRENT_SOURCE_DIR}/libebml.tar.bz2
    URL_MD5             12a3972c57f3a15246b0e5e38a215930
    # GIT_REPOSITORY      https://github.com/Matroska-Org/libebml.git
    # GIT_REMOTE_NAME     master
    CMAKE_ARGS          -DBUILD_SHARED_LIBS=YES
                        -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_OUTPUT_DIRECTORY}
    UPDATE_COMMAND      ""
    LOG_DOWNLOAD        1
    LOG_CONFIGURE       1
    LOG_BUILD           1
    LOG_INSTALL         1
)

# ExternalProject_Get_Property(ebml INSTALL_DIR)
# add_library(ebml SHARED IMPORTED ${SOURCE_DIR})
# set_target_properties(ebml PROPERTIES IMPORTED_LOCATION ${SOURCE_DIR}/.libs/libebml.so)
# add_dependencies(ebml ebml_ext)

set(EBML_INCLUDE_DIRS ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/include CACHE PATH "ebml header directory" FORCE)
message(STATUS "ebml Include directory: ${EBML_INCLUDE_DIRS}")

set(EBML_LIBRARIES ${CMAKE_INSTALL_OUTPUT_DIRECTORY}/lib CACHE PATH "ebml library directory" FORCE)
message(STATUS "ebml Library directory: ${EBML_LIBRARIES}")
