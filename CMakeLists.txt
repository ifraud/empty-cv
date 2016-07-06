cmake_minimum_required(VERSION 2.8)
project( MyCVProject )

option( WITH_CUDA "CUDA Enabled" OFF)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

find_package( OpenCV REQUIRED )
find_package( CUDA )

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${OpenCV_INCLUDE_DIRS})


if(WITH_CUDA)
  if(NOT CUDA_FOUND)
    message(FATAL_ERROR "Please install CUDA and make it available for Cmake
      before compiling the code with the WITH_CUDA flag")
  endif ()
endif ()

if(WITH_CUDA)
  cuda_add_executable( DisplayImage main.cpp)
  target_link_libraries(DisplayImage ${OpenCV_LIBS})
else ()
  add_executable( DisplayImage main.cpp)
  target_link_libraries( DisplayImage ${OpenCV_LIBS})
endif ()

