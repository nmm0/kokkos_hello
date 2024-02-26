cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

project(KokkosView CXX)

find_package(Kokkos 4.1 REQUIRED)

add_executable(view view.cpp)
target_link_libraries(view PRIVATE Kokkos::kokkos)
