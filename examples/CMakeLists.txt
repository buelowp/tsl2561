cmake_minimum_required (VERSION 3.0.0)
project (test)

file (GLOB SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.c")
file (GLOB HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/../src/*.h")

set (CMAKE_CXX_STANDARD 14)

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})
target_include_directories (${PROJECT_NAME} PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/../src")
target_link_libraries (${PROJECT_NAME} PUBLIC ${CMAKE_BINARY_DIR}/src/libtsl2561.so -li2c)
