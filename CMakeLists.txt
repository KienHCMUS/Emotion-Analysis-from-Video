cmake_minimum_required(VERSION 3.10)
project(MyOpenCVProject)

set(CMAKE_CXX_STANDARD 17)

# Find OpenCV package
find_package(OpenCV REQUIRED)

# Add executable
add_executable(MyApp main.cpp)

# Link OpenCV libraries
target_link_libraries(MyApp ${OpenCV_LIBS})

# Copy .onnx files to build directory for runtime access
file(GLOB ONNX_FILES "${CMAKE_CURRENT_SOURCE_DIR}/*.onnx")
file(COPY ${ONNX_FILES} DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/Release)