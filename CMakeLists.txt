cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
set(PICO_SDK_PATH "/Volumes/Storage/Projects/Embedded/Raspberry Pi Pico/pico-sdk")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(picoboot C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

add_executable(picoboot picoboot.c)

pico_generate_pio_header(picoboot  
        ${CMAKE_CURRENT_LIST_DIR}/picoboot.pio
)

pico_set_program_name(picoboot "picoboot")
pico_set_program_version(picoboot "0.1")
pico_set_binary_type(picoboot copy_to_ram)

pico_enable_stdio_uart(picoboot 0)
pico_enable_stdio_usb(picoboot 1)

target_link_libraries(picoboot 
    pico_stdlib
    hardware_pio
    hardware_dma
)

pico_add_extra_outputs(picoboot)