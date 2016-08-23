cmake_minimum_required(VERSION 3.0)

project(mp3lame)

add_definitions(-DHAVE_STDINT_H)
add_definitions(-DHAVE_MPGLIB)
add_definitions(-DSTDC_HEADERS)
add_definitions(-Dieee754_float32_t=float)

if (UNIX)
	add_definitions(-Wno-unused-variable)
endif(UNIX)

set(LIBMP3LAME_PATH "${CMAKE_CURRENT_SOURCE_DIR}/libmp3lame/")
set(LIBMP3LAME_SOURCES
	${LIBMP3LAME_PATH}/VbrTag.c
	${LIBMP3LAME_PATH}/bitstream.c
	${LIBMP3LAME_PATH}/encoder.c
	${LIBMP3LAME_PATH}/fft.c
	${LIBMP3LAME_PATH}/gain_analysis.c
	${LIBMP3LAME_PATH}/id3tag.c
	${LIBMP3LAME_PATH}/lame.c
	${LIBMP3LAME_PATH}/newmdct.c
	${LIBMP3LAME_PATH}/presets.c
	${LIBMP3LAME_PATH}/psymodel.c
	${LIBMP3LAME_PATH}/quantize.c
	${LIBMP3LAME_PATH}/quantize_pvt.c
	${LIBMP3LAME_PATH}/reservoir.c
	${LIBMP3LAME_PATH}/set_get.c
	${LIBMP3LAME_PATH}/tables.c
	${LIBMP3LAME_PATH}/takehiro.c
	${LIBMP3LAME_PATH}/util.c
	${LIBMP3LAME_PATH}/vbrquantize.c
	${LIBMP3LAME_PATH}/version.c
	${LIBMP3LAME_PATH}/mpglib_interface.c
	${LIBMP3LAME_PATH}/vector/xmm_quantize_sub.c)

set(MPGLIB_PATH "${CMAKE_CURRENT_SOURCE_DIR}/mpglib/")
set (MPGLIB_SOURCES
	${MPGLIB_PATH}/common.c
	${MPGLIB_PATH}/dct64_i386.c
	${MPGLIB_PATH}/decode_i386.c
	${MPGLIB_PATH}/interface.c
	${MPGLIB_PATH}/layer1.c
	${MPGLIB_PATH}/layer2.c
	${MPGLIB_PATH}/layer3.c
	${MPGLIB_PATH}/tabinit.c)

set(LAME_INCLUDE "${CMAKE_CURRENT_SOURCE_DIR}/include")
set(LAME_SOURCES ${LIBMP3LAME_SOURCES} ${MPGLIB_SOURCES})

include_directories(${LAME_INCLUDE})
include_directories(${LIBMP3LAME_PATH})
include_directories(${MPGLIB_PATH})

add_library(${PROJECT_NAME} SHARED ${LAME_SOURCES})

target_include_directories(${PROJECT_NAME} PUBLIC ${LAME_INCLUDE})
