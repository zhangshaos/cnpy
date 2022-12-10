CMAKE_MINIMUM_REQUIRED(VERSION 3.12)
project(cnpy)

if(MSVC)
    add_compile_options(/bigobj /MP /utf-8)
endif()
set(CMAKE_CXX_STANDARD 17)

find_package(ZLIB REQUIRED)
find_package(OpenCV REQUIRED)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

add_library(cnpy STATIC cnpy.cpp)
target_include_directories(cnpy PUBLIC ${PROJECT_SOURCE_DIR})
target_link_libraries(cnpy PUBLIC ZLIB::ZLIB ${OpenCV_LIBS})

###################################
#       Build c++ Example         #
###################################
set(BUILD_EXAMPLE FALSE)
if(BUILD_EXAMPLE)
add_executable(cnpy_example example.cpp)
target_link_libraries(cnpy_example cnpy)
endif()