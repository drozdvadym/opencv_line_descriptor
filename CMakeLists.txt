cmake_minimum_required(VERSION 2.8)
project(opencv_line_descriptor)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")

find_package(OpenCV REQUIRED)

include_directories(include)

file(GLOB_RECURSE LIB_HDRS "include/*.hpp")

set(LIB_SRCS
    src/binary_descriptor.cpp
    src/binary_descriptor_matcher.cpp
    src/bitarray.hpp
    src/bitops.hpp
    src/draw.cpp
    src/draw.cpp
    src/LSDDetector.cpp
    src/precomp.hpp
    src/types.hpp
    src/lsd.cpp
    )

add_library(opencv_line_descriptor SHARED ${LIB_SRCS} ${LIB_HDRS})
target_link_libraries(opencv_line_descriptor opencv_features2d opencv_imgproc opencv_highgui)

macro(ADD_SAMPLE name)
  set(_name "example_line_descriptor_${name}")
  add_executable(${_name} ${CMAKE_CURRENT_SOURCE_DIR}/samples/${name}.cpp)
  target_link_libraries(${_name} opencv_line_descriptor)
endmacro(ADD_TEST)

ADD_SAMPLE(matching)
ADD_SAMPLE(compute_descriptors)
ADD_SAMPLE(knn_matching)
ADD_SAMPLE(radius_matching)
ADD_SAMPLE(lines_extraction)
ADD_SAMPLE(lsd_lines_extraction)
