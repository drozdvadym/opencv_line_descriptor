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

macro(ADD_SAMPLE name srcs)
  add_executable(${name} ${srcs})
  target_link_libraries(${name} opencv_line_descriptor)
endmacro(ADD_TEST)

ADD_SAMPLE(test_matching             samples/matching.cpp)
ADD_SAMPLE(test_compute_descriptors  samples/compute_descriptors.cpp)
ADD_SAMPLE(test_knn_matching         samples/knn_matching.cpp)
ADD_SAMPLE(test_lines_extraction     samples/lines_extraction.cpp)
ADD_SAMPLE(test_lsd_lines_extraction samples/lsd_lines_extraction.cpp)
ADD_SAMPLE(test_radius_matching      samples/radius_matching.cpp)