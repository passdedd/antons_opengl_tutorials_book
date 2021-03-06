cmake_minimum_required(VERSION 3.6)   # CMake version check
project(antons_tutorials C CXX)               # Create project "simple_example"
set(CMAKE_CXX_STANDARD 11)            # Enable c++11 standard

#add source folder so the program can be compiled at build folder
include_directories(${CMAKE_SOURCE_DIR} "../common/include")
#include_directories(${antons_tutorials_SOURCE_DIR})


#Headers
file(GLOB HEADERS
  *.h
  *.cpp
  )

#Main
set(SOURCE_FILES main.cpp maths_funcs.cpp gl_utils.cpp)
add_executable(skin ${SOURCE_FILES} ${HEADERS})

#OpenGL
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIR})

target_link_libraries(skin ${OPENGL_gl_LIBRARY})


#GLFW
find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)
include_directories(${GLFW_INCLUDE_DIRS})
target_link_libraries(skin ${GLFW_LIBRARIES})


#ASSIMP
find_package(ASSIMP REQUIRED)
if (ASSIMP_FOUND)
    include_directories(${ASSIMP_INCLUDE_DIRS})
    target_link_libraries(skin ${ASSIMP_LIBRARIES})
  endif()

#GLEW
find_package(GLEW REQUIRED)
if (GLEW_FOUND)
    include_directories(${GLEW_INCLUDE_DIRS})
    target_link_libraries(skin ${GLEW_LIBRARIES})
  endif()




