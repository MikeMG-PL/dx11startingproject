cmake_minimum_required(VERSION 3.10)

# Set the project name
project(DX11Playground)

# Specify the build directory
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
message(STATUS "Binary directory set to: ${CMAKE_BINARY_DIR}")

# Add include directory for ImGui and its subdirectories recursively
include_directories(${CMAKE_SOURCE_DIR}/imgui-docking)
include_directories(${CMAKE_SOURCE_DIR}/imgui-docking/backends)

# Collect ImGui source files
file(GLOB IMGUI_HEADERS ${CMAKE_SOURCE_DIR}/imgui-docking/*.h)
file(GLOB IMGUI_SOURCES ${CMAKE_SOURCE_DIR}/imgui-docking/*.cpp)
file(GLOB IMGUI_BACKEND_HEADERS ${CMAKE_SOURCE_DIR}/imgui-docking/backends/*.h)
file(GLOB IMGUI_BACKEND_SOURCES ${CMAKE_SOURCE_DIR}/imgui-docking/backends/*.cpp)

# Add executable target
add_executable(DX11Playground 
    src/main.cpp 
    ${IMGUI_HEADERS} 
    ${IMGUI_SOURCES}
    ${IMGUI_BACKEND_HEADERS}
    ${IMGUI_BACKEND_SOURCES}
)

# Link against necessary libraries (if ImGui requires external libraries)
# target_link_libraries(DX11Playground ImGui)
