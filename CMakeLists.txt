cmake_minimum_required(VERSION 3.13)

project(freertos-ex)

add_executable(freertos-ex src/main.c
 )
target_include_directories(freertos-ex
  PUBLIC
  amazon-freertos/vendors/espressif/esp-idf/components/sdmmc
)
set_property(TARGET freertos-ex PROPERTY CXX_STANDARD 11)

# Tell IDF build to link against this target.
set(IDF_PROJECT_EXECUTABLE freertos-ex)

# Add amazon freertos as a subdirectory. AFR_BOARD tells which board to target.
set(AFR_BOARD espressif.esp32_wrover_kit CACHE INTERNAL "")
add_subdirectory("amazon-freertos")

# Link against the mqtt library so that we can use it. Dependencies
# linked.
target_link_libraries(freertos-ex PRIVATE AFR::mqtt)
