cmake_minimum_required(VERSION 2.8)
set (CMAKE_CXX_STANDARD 11)
project( scene_text_recognition )

# use unicode
add_definitions(-DUNICODE -D_UNICODE) 

# set library and include path
if(UNIX)
    find_package(OpenCV REQUIRED)
else()
    set(OpenCV_LIBS "C:\\opencv\\build\\x64\\vc14\\lib\\opencv_world310.lib") 
    set(OpenCV_INCLUDE_DIRS "C:\\opencv\\build\\include")
endif()

find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

file(GLOB SOURCES "src/*.cpp")
include_directories( ${OpenCV_INCLUDE_DIRS} ) 
add_executable(scene_text_recognition ${SOURCES})
target_link_libraries(scene_text_recognition ${OpenCV_LIBS})
