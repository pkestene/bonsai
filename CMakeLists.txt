cmake_minimum_required(VERSION 3.10)
project(bonsai LANGUAGES CXX CUDA)

#find_package(CUDA REQUIRED)
enable_language(CUDA)

# make CUDA use C++11 standard
if(NOT DEFINED CMAKE_CUDA_STANDARD)
  set(CMAKE_CUDA_STANDARD 11)
  set(CMAKE_CUDA_STANDARD_REQUIRED ON)
endif()
  
add_executable(bonsai
  ${CMAKE_CURRENT_SOURCE_DIR}/serial.cu
  ${CMAKE_CURRENT_SOURCE_DIR}/thrust.cu)

target_compile_features(bonsai PUBLIC cxx_std_11)
set_target_properties(bonsai PROPERTIES CUDA_SEPARABLE_COMPILATION ON)
set_target_properties(bonsai PROPERTIES POSITION_INDEPENDENT_CODE ON)
set(CMAKE_CUDA_FLAGS "-arch=sm_50 -use_fast_math")

target_link_libraries(bonsai cuda)
