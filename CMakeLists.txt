# Set the minimum required version of CMake
cmake_minimum_required(VERSION 3.14)

# Set the project name and version
project(RPGForFun VERSION 1.0)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Include FetchContent module
include(FetchContent)


# Find OpenGL package
find_package(OpenGL REQUIRED)

# Glob source and header files
file(GLOB_RECURSE SOURCES "src/*.cpp")
file(GLOB_RECURSE HEADERS "src/*.h")

# Add the executable target
add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

# Link OpenGL and GLFW to your project
target_link_libraries(${PROJECT_NAME} PRIVATE
    OpenGL::GL
)

# Optionally include directories for GLFW and OpenGL if needed
target_include_directories(${PROJECT_NAME} PRIVATE
    ${OPENGL_INCLUDE_DIR}
    ${GLFW_INCLUDE_DIRS}
    ${CMAKE_SOURCE_DIR}/include
)

# Specify the output directory for the executable
set_target_properties(${PROJECT_NAME} PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin
)
