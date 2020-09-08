cmake_minimum_required(VERSION 3.17)

project(hiredis-vip-cmake)

enable_language(C)

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

set(TARGET_NAME hiredis_vex)

add_library(${TARGET_NAME} STATIC ${TARGET_SRC})

install(DIRECTORY src/
    DESTINATION include/hiredis
    FILES_MATCHING PATTERN "*.h"
)

install(TARGETS ${TARGET_NAME} 
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)