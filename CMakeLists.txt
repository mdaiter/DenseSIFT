cmake_minimum_required(VERSION 2.8)
project(DenseSIFT)

set (CMAKE_C_COMPILER /usr/local/Cellar/llvm/8.0.1/bin/clang)
set (CMAKE_CXX_COMPILER /usr/local/Cellar/llvm/8.0.1/bin/clang++)

include_directories(${CMAKE_SOURCE_DIR})
include_directories(./include)
include_directories(/Users/msd/Downloads/vlfeat)
include_directories(/Users/msd/Downloads/cpp-taskflow)

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -stdlib=libc++")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
        set(LLVM_CONFIG true)
        set(CLANG_INCLUDEDIR "C:/Program Files (x86)/LLVM/include")
        set(CLANG_LIBDIR "C:/Program Files (x86)/LLVM/lib")
endif()

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")
find_package(OpenCV REQUIRED)
find_package (Eigen3 REQUIRED NO_MODULE)

file(GLOB SRC "src/*.cpp" "include/*.h")
add_library(densesift ${SRC})

target_link_libraries(densesift ${OpenCV_LIBS})
target_link_libraries(densesift Eigen3::Eigen)
target_link_libraries(densesift /Users/msd/Downloads/vlfeat/bin/maci64/libvl.dylib)
