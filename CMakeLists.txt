cmake_minimum_required(VERSION 3.8)

set(TARGET ctpl)
set(${TARGET}_VERSION 0.0.2)
project(${TARGET} VERSION ${${TARGET}_VERSION} LANGUAGES CXX)

option(CTPL_EXAMPLE "Build CTPL example" OFF)

add_library(${TARGET} INTERFACE)
add_library(${TARGET}::${TARGET} ALIAS ${TARGET})

target_sources(${TARGET} INTERFACE
  ${CMAKE_CURRENT_LIST_DIR}/include/ctpl/ctpl.h
  ${CMAKE_CURRENT_LIST_DIR}/include/ctpl/ctpl_stl.h
)

find_package(Threads REQUIRED)
target_link_libraries(ctpl INTERFACE Threads::Threads)

if (CTPL_EXAMPLE)
  add_executable(ctpl_example example.cpp)
  target_link_libraries(ctpl_example PRIVATE ctpl)
endif ()

include(GNUInstallDirs)

target_include_directories(${TARGET} INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/${CMAKE_INSTALL_INCLUDEDIR}>
)

