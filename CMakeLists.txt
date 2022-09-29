cmake_minimum_required(VERSION 2.8)
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../cmake)
include(GoProCommon)

SET(CMAKE_SKIP_BUILD_RPATH TRUE)
SET(CMAKE_SKIP_RPATH TRUE)
set(CMAKE_BUILD_RPATH "")
set(CMAKE_INSTALL_RPATH "")
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH FALSE)
SET(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE)

set(PROJ_NAME RtspServer)
string(TOUPPER ${PROJ_NAME} PROJ_UPPER)
project(${PROJ_NAME})

#if(${SYSTEM_NAME} MATCHES "linux-arm-")
#    # need this so 32 bit linux builds can access >2GB files
#    add_definitions(-D_FILE_OFFSET_BITS=64)
#elseif(${SYSTEM_NAME} MATCHES "linux-x86")
#    # need this so 32 bit linux builds can access >2GB files
#    add_definitions(-D_FILE_OFFSET_BITS=64)
#endif()

add_definitions(-DCRYPTO=OPENSSL)
set(${PROJ_UPPER}_LIBRARY_TYPE SHARED)

set(${PROJ_UPPER}_INCLUDE_DIRS
        src/3rdpart
        src
        )

set(${PROJ_UPPER}_LIBRARY_DIRS
    ${CMAKE_SOURCE_DIR}/../banzailink_ep/staging/${SCS_NAME}/sys_root/usr/lib
   )

set(${PROJ_UPPER}_LINK_LIBRARIES
        rt
        pthread
        dl
        m
   )

SET(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -std=c++11")
SET(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -std=c++11")

set(${PROJ_UPPER}_SOURCES
    src/xop/AACSource.cpp
    src/xop/DigestAuthentication.cpp
    src/xop/G711ASource.cpp
    src/xop/H264Parser.cpp
    src/xop/H264Source.cpp
    src/xop/H265Source.cpp
    src/xop/MediaSession.cpp
    src/xop/RtpConnection.cpp
    src/xop/RtspConnection.cpp
    src/xop/RtspMessage.cpp
    src/xop/RtspPusher.cpp
    src/xop/RtspServer.cpp
    src/xop/VP8Source.cpp

    src/net/Acceptor.cpp
    src/net/BufferReader.cpp
    src/net/BufferWriter.cpp
    src/net/EpollTaskScheduler.cpp
    src/net/EventLoop.cpp
    src/net/Logger.cpp
    src/net/MemoryManager.cpp
    src/net/NetInterface.cpp
    src/net/Pipe.cpp
    src/net/SelectTaskScheduler.cpp
    src/net/SocketUtil.cpp
    src/net/TaskScheduler.cpp
    src/net/TcpConnection.cpp
    src/net/TcpServer.cpp
    src/net/TcpSocket.cpp
    src/net/Timer.cpp
    src/net/Timestamp.cpp
    )

add_gopro_library(${PROJ_NAME})

