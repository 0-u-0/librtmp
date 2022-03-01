cmake_minimum_required(VERSION 3.21)
project(rtmp C)


# set(OPENSSL_ROOT_DIR "/usr/local/Cellar/openssl@1.1/1.1.1l_1")
# find_package (OpenSSL)


set(PROJECT_ROOT_PATH ${CMAKE_CURRENT_SOURCE_DIR})
set(SRC_PATH ${PROJECT_ROOT_PATH}/src)

set(LIBRTMP_INC_DIR ${SRC_PATH})

function(add_src_to_var VAR)
  set(headers ${${VAR}})
  foreach (header ${ARGN})
    set(headers ${headers} ${SRC_PATH}/${header})
  endforeach()
  set(${VAR} ${headers} PARENT_SCOPE)
endfunction()
  

add_src_to_var(LIBRTMP_SOURCES rtmp.c log.c amf.c hashswf.c parseurl.c)
add_src_to_var(LIBRTMP_HEADERS amf.h http.h log.h rtmp.h)

message("" ${LIBRTMP_HEADERS})
add_library(${PROJECT_NAME} ${LIBRTMP_SOURCES} ${LIBRTMP_HEADERS})

target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${SRC_PATH}>  # for deps package
  $<INSTALL_INTERFACE:${LIBRTMP_INC_DIR}>)

target_compile_definitions(${PROJECT_NAME} PRIVATE "NO_CRYPTO")
# target_include_directories(${PROJECT_NAME} SYSTEM PUBLIC ${OPENSSL_INCLUDE_DIRS})
# target_link_libraries(${PROJECT_NAME} ${OPENSSL_LIBRARIES})

