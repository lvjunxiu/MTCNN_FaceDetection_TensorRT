cmake_minimum_required(VERSION 3.5)
project(main)

add_definitions(-std=c++11)
#set(QMAKE_CXXFLAGS "-std=c++11")
include_directories(/opt/OpenBLAS/include)
include_directories(/usr/local/cuda/include)
include_directories(/home/zhou/tensorrt/include)
link_directories(/home/zhou/tensorrt/lib)
link_directories(/opt/cuda/lib64)

find_package( OpenCV REQUIRED)

AUX_SOURCE_DIRECTORY(./src DIR_SRCS)
add_executable( main ${DIR_SRCS} src/pnet_rt.cpp src/common.h src/common.cpp src/pnet_rt.h src/rnet_rt.cpp src/rnet_rt.h src/baseEngine.cpp src/baseEngine.h src/onet_rt.h src/onet_rt.cpp)

set(CMAKE_CXX_FLAGS  "-lpthread")
set(CMAKE_CXX_FLAGS  "-O3")
target_link_libraries( main ${OpenCV_LIBS} )
target_link_libraries( main openblas)
target_link_libraries( main cudart)
target_link_libraries( main nvinfer)
target_link_libraries( main nvparsers)


