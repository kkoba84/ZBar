set(projname "zbar")

project(${projname})

include_directories("c:/Anaconda/include")
link_directories("c:/Anaconda/libs")
FIND_PACKAGE(PythonLibs)

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
set_target_properties(${projname} PROPERTIES SUFFIX ".pyd")
target_link_libraries(${projname} libzbar python27)



	