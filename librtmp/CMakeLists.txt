cmake_minimum_required(VERSION 3.21)
project(librtmp C)


# set(OPENSSL_ROOT_DIR "/usr/local/Cellar/openssl@1.1/1.1.1l_1")
# find_package (OpenSSL)

set_verbose(LIBRTMP_INC_DIR ${CMAKE_INSTALL_INCLUDEDIR} CACHE STRING
            "Installation directory for include files, a relative path that "
            "will be joined with ${CMAKE_INSTALL_PREFIX} or an absolute path.")

set(LIBRTMP_SOURCES rtmp.c log.c amf.c hashswf.c parseurl.c)
set(LIBRTMP_HEADERS amf.h http.h log.h rtmp.h)

add_library(${PROJECT_NAME} ${LIBRTMP_SOURCES} ${LIBRTMP_HEADERS})

target_include_directories(${PROJECT_NAME} PUBLIC
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:${LIBRTMP_INC_DIR}>)

target_compile_definitions(${PROJECT_NAME} PRIVATE "NO_CRYPTO")
# target_include_directories(${PROJECT_NAME} SYSTEM PUBLIC ${OPENSSL_INCLUDE_DIRS})
# target_link_libraries(${PROJECT_NAME} ${OPENSSL_LIBRARIES})

