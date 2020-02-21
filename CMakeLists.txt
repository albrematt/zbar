cmake_minimum_required(VERSION 3.1.2)

project(zbar VERSION 0.23 LANGUAGES C)

option(ZBAR_BUILD_EXAMPLE "Enable to build zbar example" OFF)

include(GNUInstallDirs)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_BINDIR})

add_library(zbar STATIC
		include/zbar.h
		src/config.h
		src/decoder.h
		src/image.h
		src/img_scanner.h
		src/scanner.c
		src/symbol.h
		src/decoder.c
		src/image.c
		src/img_scanner.c
		src/qrcode.h
		src/symbol.c
		src/decoder/codabar.c
		src/decoder/code128.c
		src/decoder/code39.c
		src/decoder/code93.c
		src/decoder/databar.c
		src/decoder/ean.c
		src/decoder/i25.c
		src/decoder/pdf417.c
		src/decoder/pdf417_hash.h
		src/decoder/qr_finder.h
		src/decoder/codabar.h
		src/decoder/code128.h
		src/decoder/code39.h
		src/decoder/code93.h
		src/decoder/databar.h
		src/decoder/ean.h
		src/decoder/i25.h
		src/decoder/pdf417.h
		src/decoder/qr_finder.c
		src/decoder/qrcode/bch15_5.c
		src/decoder/qrcode/binarize.c
		src/decoder/qrcode/isaac.c
		src/decoder/qrcode/qrdec.c
		src/decoder/qrcode/qrdectxt.c
		src/decoder/qrcode/rs.h
		src/decoder/qrcode/util.h
		src/decoder/qrcode/bch15_5.h
		src/decoder/qrcode/binarize.h
		src/decoder/qrcode/isaac.h
		src/decoder/qrcode/qrdec.h
		src/decoder/qrcode/rs.c
		src/decoder/qrcode/util.c
		)

set_target_properties(zbar PROPERTIES 
		FOLDER External
		)
target_compile_features(zbar PUBLIC c_std_11)
target_include_directories(zbar PUBLIC
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
		PRIVATE
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
		)

if(ZBAR_BUILD_EXAMPLE)
	add_executable(zbar_example example/stb_image.h example/test.c)
	target_link_directories(zbar_example PRIVATE zbar)
endif()
