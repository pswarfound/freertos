INCLUDE_DIRECTORIES(./CMSIS)
INCLUDE_DIRECTORIES(./os)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/freertos/include)

aux_source_directory(./CMSIS _SRC)
aux_source_directory(./os/ _SRC)

ADD_library(hal STATIC ${_SRC})
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)


add_custom_command(TARGET hal PRE_BUILD
COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_SOURCE_DIR}/hal/mec17xx/CMSIS/sections.ld ${PROJECT_BINARY_DIR}/lib/
COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_SOURCE_DIR}/hal/mec17xx/os/FreeRTOSConfig.h ${PROJECT_SOURCE_DIR}/include/hal
COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_SOURCE_DIR}/hal/mec17xx/os/portmacro.h ${PROJECT_SOURCE_DIR}/include/hal
)
