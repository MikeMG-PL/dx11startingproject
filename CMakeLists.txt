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

# Include CPM module
include(cmake/CPM.cmake)

# Define GLM version
set(GLM_VERSION 1.0.1)

set(GLM_INCLUDE_DIRS ${CMAKE_BINARY_DIR}/_deps/glm-src/)

# Use CPM to fetch and configure GLM
CPMAddPackage(
    NAME GLM
    VERSION ${GLM_VERSION}
    URL https://github.com/g-truc/glm/archive/${GLM_VERSION}.tar.gz
)

# Add executable target
add_executable(DX11Playground 
    src/main.cpp 
    ${IMGUI_HEADERS} 
    ${IMGUI_SOURCES}
    ${IMGUI_BACKEND_HEADERS}
    ${IMGUI_BACKEND_SOURCES}
    ${GLM_INCLUDE_DIRS}
)

# Add include directory for GLM
include_directories(${GLM_INCLUDE_DIRS})

# Add directory "include" for .h files
include_directories(${CMAKE_SOURCE_DIR}/include)

# Link against necessary libraries (if ImGui requires external libraries)
target_link_libraries(DX11Playground ImGui)
