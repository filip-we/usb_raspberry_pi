cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

set(PICO_PLATFORM rp2040)
set(FAMILY rp2040)
set(BOARD pico_sdk)
set(TINYUSB_FAMILY_PROJECT_NAME_PREFIX "tinyusb_dev_")
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

project(usb_test C CXX ASM)

add_executable(usb_test)

target_sources(usb_test PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/main.c
    ${CMAKE_CURRENT_LIST_DIR}/usb_descriptors.c
)

target_include_directories(usb_test PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}
)

target_link_libraries(usb_test PUBLIC
    pico_stdlib
    tinyusb_device
    tinyusb_board
)

pico_sdk_init()

pico_enable_stdio_usb(usb_test 0)
pico_enable_stdio_uart(usb_test 1)
pico_add_extra_outputs(usb_test)

