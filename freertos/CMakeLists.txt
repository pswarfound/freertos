INCLUDE_DIRECTORIES(./include)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/include/hal)

aux_source_directory(./ _SRC)

ADD_library(freertos STATIC ${_SRC})
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
add_dependencies(freertos hal)

