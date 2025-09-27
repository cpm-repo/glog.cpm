cmake_minimum_required(VERSION 3.14)

project(gflags.cpm)

if(PROJECT_IS_TOP_LEVEL)
  file(DOWNLOAD https://github.com/cpm-cmake/CPM.cmake/releases/latest/download/CPM.cmake
       ${CMAKE_CURRENT_BINARY_DIR}/cmake/CPM.cmake
  )
  include(${CMAKE_CURRENT_BINARY_DIR}/cmake/CPM.cmake)
endif()

get_property(
  CPM_INITIALIZED GLOBAL
  PROPERTY CPM_INITIALIZED
  SET
)

if(NOT CPM_INITIALIZED)
  message(FATAL "You should include CPM.cmake frist")
endif()

CPMAddPackage("gh:cpm-repo/gflags.cpm@2.2.2")
CPMAddPackage(
  NAME glog
  VERSION 0.7.1
  URL https://github.com/google/glog/archive/refs/tags/v0.7.1.tar.gz
  PATCHES ./fe6edce426c9a1bcc83bc3b3b50ca95b3cc60c21.patch
  EXCLUDE_FROM_ALL YES
  SYSTEM NO
  OPTIONS "SKIP_INSTALL ON"
)

if(NOT PROJECT_IS_TOP_LEVEL)
  return()
endif()

add_subdirectory(examples)
