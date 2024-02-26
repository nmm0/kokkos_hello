cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

project(KokkosView CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Future logic:
# if CUDA, nvcc_wrapper; elif HIP, gcc + hipcc; else serial(?)
# CUDA
# Set each variable below according to your machine
set(CUDA_ROOT /home/projects/x86-64/cuda/12.0)
set(CUDA_LIB /home/projects/x86-64/cuda/12.0/lib64)
set(CUDA_INCLUDE /home/projects/x86-64/cuda/12.0/include)
set(KOKKOS_ROOT /ascldap/users/ajpowel/view_for_documentation/kokkos)
#set(KOKKOS_INSTALL /ascldap/users/ajpowel/view_for_documentation/kokkos_install_cuda)
set(KOKKOS_INSTALL /ascldap/users/ajpowel/view_for_documentation/kokkos_install_serial)
set(KOKKOS_LIB ${KOKKOS_INSTALL}/lib64/libkokkoscore.so)
set(KOKKOS_INCLUDE ${KOKKOS_INSTALL}/include)


# HIP
# Forthcoming
include_directories(${KOKKOS_INCLUDE})

option(Kokkos_ENABLE_CUDA "Build Kokkos for CUDA Backend" OFF)

option(Kokkos_ENABLE_ "Build Kokkos for HIP Backend" OFF)

if(Kokkos_ENABLE_CUDA)
  message(STATUS "Building Kokkos with CUDA Backend ... ")
  add_definitions(-DKokkos_ENABLE_CUDA)
# Use `nvcc_wrapper` to compile CUDA code; gcc or clang can be the underlying
# CPU compiler
  set(CMAKE_CXX_COMPILER ${KOKKOS_ROOT}/bin/nvcc_wrapper)
  set(CMAKE_CXX_FLAGS "--extended-lambda")
  include_directories(${CUDA_INCLUDE})
  add_executable(view_exe_cuda view.cpp)
  target_link_libraries(view_exe_cuda
                        ${KOKKOS_LIB}
                        ${CUDA_LIB}/libcudart.so)
  set_target_properties(view_exe_cuda PROPERTIES
                        CXX_STANDARD 17
                        CXX_EXTENSIONS OFF
                       )
elseif(Kokkos_ENABLE_HIP)
  message(STATUS "Building Kokkos with HIP Backend FORTHCOMING ...")
  MESSAGE(FATAL " HIP NOT READY YET: ~~~~~~~~~~~~~~~~~~~~~~${CXX_COMPILER}") 
  add_definitions(-DKokkos_ENABLE_HIP)
  #set(CMAKE_CXX_FLAGS "--extended-lambda")
  #include_directories(${CUDA_INCLUDE})
  #add_executable(view_exe_cuda view.cpp)
  #target_link_libraries(view_exe
  #                      ${KOKKOS_LIB}
  #                      ${CUDA_LIB}/libcudart.so)
  #set_target_properties(view_exe_cuda PROPERTIES
  #                      CXX_STANDARD 17
  #                      CXX_EXTENSIONS OFF
  #                     )
elseif(Kokkos_ENABLE_SERIAL)
    message(STATUS "Building Kokkos for Serial Computation FORTHCOMING ...")
    add_definitions(-DKokkos_ENABLE_SERIAL)
    set(CMAKE_CXX_COMPILER g++)
    set(CMAKE_CXX_FLAGS "-std=c++17")
    add_executable(view_exe_serial view.cpp)
    target_link_libraries(view_exe_serial
                        ${KOKKOS_LIB})
    set_target_properties(view_exe_serial PROPERTIES
                          CXX_STANDARD 17
                          CXX_EXTENSIONS OFF
                         )
endif()


