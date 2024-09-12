cmake_minimum_required(VERSION 3.10)
project(JoyConBridge)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)

# Specify the build configurations
set(CMAKE_CONFIGURATION_TYPES "Debug;Release" CACHE STRING "Configurations" FORCE)

# Define the source files
set(SRC_FILES
    command_ids.cpp
    connect.cpp
    exceptions.cpp
    HidDevice.cpp
    JoyCon.cpp
    protocol.cpp
    strings.cpp
)

# Define the header files
set(HEADER_FILES
    Buffer.h
    command_ids.h
    connect.h
    exceptions.h
    HidDevice.h
    JoyCon.h
    protocol.h
    strings.h
)

# Create a static library (you can also choose SHARED for a dynamic library)
add_library(JoyConBridge STATIC ${SRC_FILES} ${HEADER_FILES})

# Include the JoyConBridge source directory
target_include_directories(JoyConBridge PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Include hidapi
add_subdirectory(hidapi)
target_include_directories(JoyConBridge PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/hidapi/hidapi)
target_link_libraries(JoyConBridge PRIVATE hidapi)