cmake_minimum_required(VERSION 2.8)
include(CheckIncludeFile)

set(SAMP lws-minimal-ws-client-tx)
set(SRCS minimal-ws-client.c)

if (UNIX)
      set(CMAKE_C_FLAGS "-Wall -Wsign-compare -Wignored-qualifiers -Wtype-limits -Wuninitialized -Werror -Wundef ${CMAKE_C_FLAGS}" )
endif()

CHECK_INCLUDE_FILE(pthread.h LWS_HAVE_PTHREAD_H)
if (NOT LWS_HAVE_PTHREAD_H)
	message(FATAL_ERROR "threading support requires pthreads")
endif()

add_executable(${SAMP} ${SRCS})
target_link_libraries(${SAMP} -lwebsockets -pthread)

