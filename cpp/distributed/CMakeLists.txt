cmake_minimum_required(VERSION 3.1 FATAL_ERROR)
project(dist-mnist)

set(CMAKE_PREFIX_PATH "/home/chen/pytorch/install")
set(CMAKE_CUDA_COMPILER "/usr/local/cuda/bin/nvcc")
set(CMAKE_CXX_STANDARD 17)

find_package(Torch REQUIRED)

find_package(MPI REQUIRED)

include_directories(SYSTEM ${MPI_C_INCLUDE_PATH} ${MPI_CXX_INCLUDE_PATH})
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${TORCH_CXX_FLAGS}")

add_executable(dist-mnist dist-mnist.cpp)
target_link_libraries(dist-mnist ${TORCH_LIBRARIES})
target_link_libraries(dist-mnist ${MPI_LIBRARIES})
#target_link_libraries(dist-mnist ${CMAKE_PREFIX_PATH}/lib/libc10d.a)


set_target_properties(dist-mnist PROPERTIES
    COMPILE_FLAGS "${MPI_COMPILE_FLAGS}")



set_target_properties(dist-mnist PROPERTIES
    LINK_FLAGS "${MPI_LINK_FLAGS}")
