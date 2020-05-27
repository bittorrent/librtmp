cmake_minimum_required(VERSION 3.10)

project(librtmp C)

add_definitions(
-DUSE_OPENSSL
-D_CRT_SECURE_NO_WARNINGS
)

set(SRCS
	librtmp/amf.h
	librtmp/bytes.h
	librtmp/dh.h
	librtmp/dhgroups.h
	librtmp/handshake.h
	librtmp/http.h
	librtmp/log.h
	librtmp/rtmp.h
	librtmp/rtmp_sys.h
	librtmp/amf.c
	librtmp/hashswf.c
	librtmp/log.c
	librtmp/parseurl.c
	librtmp/rtmp.c
)
find_package(OpenSSL REQUIRED)
find_package(ZLib REQUIRED)

include_directories(
	${CMAKE_SOURCE_DIR}/include
	${CMAKE_SOURCE_DIR}/librtmp
	${OPENSSL_INCLUDE_DIR}
	${ZLIB_INCLUDE_DIRS}
)

add_library(librtmp SHARED
	${SRCS}
)

target_link_libraries(librtmp ${OPENSSL_LIBRARIES} ${ZLIB_LIBRARIES} Ws2_32 winmm gdi32)

target_compile_options(
	librtmp
	PRIVATE -DEXPORT
)

target_link_libraries(librtmp)
