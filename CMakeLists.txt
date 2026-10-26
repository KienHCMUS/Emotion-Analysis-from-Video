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
if(CMAKE_CONFIGURATION_TYPES)
    # For multi-config: copy to Debug/Release folder
    foreach(OUTPUT_CONFIG ${CMAKE_CONFIGURATION_TYPES})
        file(COPY ${ONNX_FILES} DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/${OUTPUT_CONFIG})
    endforeach()
else()
    # For single-config: copy to build folder
    file(COPY ${ONNX_FILES} DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
endif()