INCLUDE_DIRECTORIES(./include)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/freertos/include)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/include/hal)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/hal/mec17xx/CMSIS)

aux_source_directory(./ _SRC)

LINK_DIRECTORIES(${PROJECT_BINARY_DIR}/lib)

add_executable(app ${_SRC})

TARGET_LINK_LIBRARIES(app
    -Wl,--whole-archive
    hal
    -Wl,--no-whole-archive
    freertos
)
add_dependencies(app freertos hal)
