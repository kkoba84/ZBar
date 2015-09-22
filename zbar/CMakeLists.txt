set(projname "libzbar")

project(${projname})

set(hdrs debug.h
		error.h
		symbol.h
		image.h
		processor.h
		refcnt.h
		timer.h
		mutex.h
		event.h
		thread.h
		window.h
		video.h
		img_scanner.h
		decoder.h
)

set(srcs config.c
		error.c
		symbol.c
		image.c
		convert.c
		processor.c
		processor/lock.c
		refcnt.c
		window.c
		video.c
		img_scanner.c
		scanner.c
		decoder.c
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

if (ENABLE_EAN)
	list(APPEND srcs "decoder/ean.c")
	list(APPEND hdrs "decoder/ean.h")
endif()

if (ENABLE_DATABAR)
	list(APPEND hdrs "decoder/databar.h")
	list(APPEND srcs "decoder/databar.c")
endif()

if (ENABLE_CODE128)
	list(APPEND hdrs "decoder/code128.h")
	list(APPEND srcs "decoder/code128.c")
endif()

if (ENABLE_CODE93)
	list(APPEND hdrs "decoder/code93.h")
	list(APPEND srcs "decoder/code93.c")
endif()

if (ENABLE_CODE39)
	list(APPEND hdrs "decoder/code39.h")
	list(APPEND srcs "decoder/code39.c")
endif()

if (ENABLE_CODABAR)
	list(APPEND hdrs "decoder/codabar.h")
	list(APPEND srcs "decoder/codabar.c")
endif()

if (ENABLE_I25)
	list(APPEND hdrs "decoder/i25.h")
	list(APPEND srcs "decoder/i25.c")
endif()

if (ENABLE_PDF417)
	list(APPEND hdrs "decoder/pdf417.h decoder/pdf417_hash.h")
	list(APPEND srcs "decoder/pdf417.c")
endif()

if (ENABLE_QRCODE)
	list(APPEND hdrs "qrcode.h")
	list(APPEND hdrs "decoder/qr_finder.h")
	list(APPEND srcs "decoder/qr_finder.c")
	file(GLOB qrcode_srcs "qrcode/*.c")
	file(GLOB qrcode_hdrs "qrcode/*.h")
	list(APPEND hdrs ${qrcode_hdrs})
	list(APPEND srcs ${qrcode_srcs})
endif()

file(GLOB decoder_srcs "decoder/*.c")
file(GLOB decoder_hdrs "decoder/*.h")

if (MSVC)
	add_definitions("-D_CRT_SECURE_NO_DEPRECATE -D_CRT_NONSTDC_NO_DEPRECATE")
	set(WIN_DEPEND_LIB "winmm" "gdi32" "vfw32")

	list(APPEND srcs "processor/win.c")
	list(APPEND srcs "window/win.c")
	list(APPEND srcs "window/dib.c")
	list(APPEND hdrs "window/win.h")
	list(APPEND srcs "video/vfw.c")
endif()


source_group("include" FILES ${hdrs})
source_group("src" FILES ${srcs})




add_library(${projname} STATIC 	${srcs} ${hdrs} )
target_link_libraries(${projname} iconv ${WIN_DEPEND_LIB})




