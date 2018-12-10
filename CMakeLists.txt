cmake_minimum_required(VERSION 2.8.12)
project(libzmq_catkin)

find_package(catkin REQUIRED)

add_compile_options(-std=c++11)

include(ExternalProject)
ExternalProject_Add(libzmq
    URL https://github.com/zeromq/libzmq/archive/v4.3.0.tar.gz
    URL_MD5 e92a3769533252120c4b745390aa23d9
    UPDATE_COMMAND ""
    CMAKE_ARGS -DBUILD_TESTS:BOOL=OFF -DENABLE_DRAFTS:BOOL=ON -DCMAKE_INSTALL_PREFIX:PATH=${CATKIN_DEVEL_PREFIX}
)
ExternalProject_Add(cppzmq
    URL https://github.com/zeromq/cppzmq/archive/v4.3.0.tar.gz
    URL_MD5 333b791d047c5ab6a60d8103284dedf5
    SOURCE_DIR ${PROJECT_BINARY_DIR}/cppzmq
    UPDATE_COMMAND ""
    CONFIGURE_COMMAND ""
    BUILD_COMMAND ""
    INSTALL_COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_BINARY_DIR}/cppzmq/zmq.hpp ${CATKIN_DEVEL_PREFIX}/include/
    DEPENDS libzmq
)

if(IS_DIRECTORY ${CMAKE_INSTALL_PREFIX})
    message(WARNING "Compiling for install workspace (${CMAKE_INSTALL_PREFIX})")
    catkin_package(
        INCLUDE_DIRS include/
        LIBRARIES zmq
)
else()
    message(WARNING "Compiling for devel workspace")
    file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)
    catkin_package(
        INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/
        LIBRARIES zmq
    )
endif()

install(
    DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/
    DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
install(
    DIRECTORY ${CATKIN_DEVEL_PREFIX}/lib/
    DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
