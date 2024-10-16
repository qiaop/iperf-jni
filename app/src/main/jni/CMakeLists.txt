cmake_minimum_required(VERSION 3.4.1)

#file(GLOB variable [RELATIVE path] [globbing expressions]...)
#GLOB选项将会为所有匹配查询表达式的文件生成一个文件list，并将该list存储进变量variable里
file(GLOB IPERF3_C_SOURCES
        iperf-3.17.1/src/cjson.c
        iperf-3.17.1/src/dscp.c
        iperf-3.17.1/src/iperf_api.c
        iperf-3.17.1/src/iperf_auth.c
        iperf-3.17.1/src/iperf_client_api.c
        iperf-3.17.1/src/iperf_error.c
        iperf-3.17.1/src/iperf_locale.c
        iperf-3.17.1/src/iperf_pthread.c
        iperf-3.17.1/src/iperf_sctp.c
        iperf-3.17.1/src/iperf_server_api.c
        iperf-3.17.1/src/iperf_tcp.c
        iperf-3.17.1/src/iperf_time.c
        iperf-3.17.1/src/iperf_udp.c
        iperf-3.17.1/src/iperf_util.c
        iperf-3.17.1/src/main.c
        iperf-3.17.1/src/net.c
#        iperf-3.17.1/src/t_api.c
#        iperf-3.17.1/src/t_auth.c
#        iperf-3.17.1/src/t_timer.c
#        iperf-3.17.1/src/t_units.c
#        iperf-3.17.1/src/t_uuid.c
        iperf-3.17.1/src/tcp_info.c
        iperf-3.17.1/src/timer.c
        iperf-3.17.1/src/units.c)

file(GLOB JNI_C_SOURCES
        common_jni_util.c
        iperf3_java_callback.c
        iperf3_jni_api.c)

include_directories(iperf-3.17.1/src)

SET(CMAKE_SYSTEM_NAME Android)
# API level
set(CMAKE_SYSTEM_VERSION 21)

set(CMAKE_C_FLAGS_RELEASE "-pie -fPIE -fPIC -s")
SET(CMAKE_BUILD_TYPE "Release")

######## 编译 so 库 ########
add_library(iperf3 SHARED ${IPERF3_C_SOURCES} ${JNI_C_SOURCES})
target_link_libraries( # Specifies the target library.
        iperf3

        # Links the target library to the log library
        # included in the NDK.
        log)

######## 编译可执行文件 ########
#add_executable(iperf3 ${IPERF3_C_SOURCES})
