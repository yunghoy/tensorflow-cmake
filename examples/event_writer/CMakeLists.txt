cmake_minimum_required( VERSION 2.8 )

project( TFCustomOp )

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/../../cmake/modules)
find_package(TensorFlow 1.10 EXACT REQUIRED)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_GLIBCXX_USE_CXX11_ABI=${TensorFlow_ABI}")
set(CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} -D_GLIBCXX_USE_CXX11_ABI=${TensorFlow_ABI}" )

TensorFlow_REQUIRE_C_LIBRARY()
TensorFlow_REQUIRE_SOURCE()

include_directories($ENV{TENSORFLOW_SRC_DIR})
add_executable(write_events write_events.cpp)
target_include_directories(write_events PRIVATE TensorFlow_DEP)
target_link_libraries(write_events PRIVATE TensorFlow_DEP)
