cmake_minimum_required(VERSION 3.12)

project(liblz4
    VERSION 1.0.0
    LANGUAGES C
)

# Set C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Platform detection
if(WIN32)
    set(PLATFORM_NAME "win32")
elseif(APPLE)
    set(PLATFORM_NAME "macos")
else()
    set(PLATFORM_NAME "linux")
endif()

# Output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin/${PLATFORM_NAME})

# Collect source files
file(GLOB LZ4_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.c
)

# Create static library
add_library(lz4 STATIC ${LZ4_SOURCES})

# Include directories
target_include_directories(lz4
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/include
)

# Compiler flags
if(NOT MSVC)
    target_compile_options(lz4 PRIVATE -Wall -Wno-unused-value -Wno-unused-but-set-variable -fPIC)
endif()
