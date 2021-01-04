cmake_minimum_required(VERSION 3.10)

project(hiredis-vip-cmake)

enable_language(C)

set(TARGET_NAME hiredis_vex)

# Option
option(CLUSTER_PROXY_16383_ALL "When Proxy return node's slot range is 0-16383" ON)

set(CMAKE_C_STANDARD 99)

set(WARNINGS "-Wall -Wextra -Werror -W -Wstrict-prototypes -Wwrite-strings -Wno-unused-function")
set(CMAKE_C_FLAGS "${WARNINGS} ${CMAKE_C_FLAGS}")
add_definitions(-DCLUSTER_PROXY_16383_ALL=${CLUSTER_PROXY_16383_ALL})
# message(${CLUSTER_PROXY_16383_ALL})
message("cflags: " ${CMAKE_C_FLAGS})

include_directories(src)

set(TARGET_SRC
src/adlist.c
src/async.c
src/command.c
src/crc16.c
src/dict.c
src/hiarray.c
src/rediscluster.c
src/hiredis.c
src/hiutil.c
src/net.c
src/read.c
src/sds.c
)

add_library(${TARGET_NAME} STATIC ${TARGET_SRC})

install(DIRECTORY src/
    DESTINATION include/hiredis
    FILES_MATCHING PATTERN "*.h"
)

install(TARGETS ${TARGET_NAME} 
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
