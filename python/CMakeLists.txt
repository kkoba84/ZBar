set(projname "zbarpy")

project(${projname})

set(srcs zbarmodule.c
	enum.c
	exception.c
	symbol.c
	symbolset.c
	symboliter.c
	image.c
	processor.c
	imagescanner.c
	decoder.c
	scanner.c
)

set(hdrs zbarmodule.h)

source_group("include" FILES ${hdrs})
source_group("src" FILES ${srcs})

add_library(${projname} SHARED ${srcs} ${hdrs})
target_link_libraries(${projname} libzbar)



	