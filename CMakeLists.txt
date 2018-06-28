cmake_minimum_required(VERSION 2.8)
project(minimal)

set(can_use_assembler TRUE)
ENABLE_LANGUAGE(ASM)

set(CMAKE_C_COMPILER arm-none-eabi-gcc)
set(CMAKE_SYSTEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR arm)
set(CMAKE_CROSSCOMPILING TRUE)
set(CMAKE_C_COMPILER arm-none-eabi-gcc)
set(CMAKE_CXX_COMPILER arm-none-eabi-c++)
set(CMAKE_STRIP arm-none-eabi-strip)
set(CMAKE_ASM_COMPILER arm-none-eabi-as)
set(CMAKE_RANLIB arm-none-eabi-ranlib)
set(CMAKE_AR arm-none-eabi-ar)

set(CMAKE_ASM_NASM_SOURCE_FILE_EXTENSIONS S)
set(CMAKE_SHARED_LIBRARY_LINK_C_FLAGS "")
set(CMAKE_SHARED_LIBRARY_LINK_CXX_FLAGS "")

add_definitions(-DDEBUG)
add_definitions(-DTRACE)
add_definitions(-DOS_USE_TRACE_SEMIHOSTING_DEBUG)
add_compile_options(-mcpu=cortex-m4 -mthumb -mfloat-abi=soft -Og -fmessage-length=0 -fsigned-char -ffreestanding -fno-move-loop-invariants -Wall -Wextra  -g3 -Wno-missing-declarations -MMD -MP)

set(CMAKE_EXE_LINKER_FLAGS
"-mcpu=cortex-m7 -mthumb -mfloat-abi=soft \
-fmessage-length=0 -fsigned-char -ffreestanding -fno-move-loop-invariants \
-Wall -Wextra \
-g3 \
-T sections.ld \
-nostartfiles -Xlinker -L${PROJECT_BINARY_DIR}/lib --specs=nano.specs"
)

INCLUDE_DIRECTORIES(${PROJECT_SRC_DIR}/freertos/include)

add_subdirectory(hal)
add_subdirectory(freertos)
add_subdirectory(app)

