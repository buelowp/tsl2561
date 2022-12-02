cmake_minimum_required (VERSION 3.0.0)
project (tsl2561)

option (TSL2561_BUILD_SHARED "Build as a shared object (default ON)" ON)

file (GLOB SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.c")
file (GLOB HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/*.h")

set (CMAKE_CXX_STANDARD 14)

set(PROJ_VERSION_MAJOR 1)
set(PROJ_VERSION_MINOR 0)
set(PROJ_VERSION_PATCH 0)
set(PROJ_VERSION ${PROJ_VERSION_MAJOR}.${PROJ_VERSION_MINOR}.${PROJ_VERSION_PATCH} )

if (TSL2561_BUILD_SHARED)
    add_library (${PROJECT_NAME} SHARED ${SOURCES})
    set_target_properties(${PROJECT_NAME} PROPERTIES VERSION ${PROJ_VERSION} SOVERSION ${PROJ_VERSION_MAJOR} )
else()
    add_library (${PROJECT_NAME} STATIC ${SOURCES})
endif()

target_link_libraries(${PROJECT_NAME} -li2c)
#target_compile_definitions(${PROJECT_NAME} PUBLIC __TSL2561_DEBUG__)

install (TARGETS ${PROJECT_NAME} DESTINATION lib)
install (FILES ${HEADERS} DESTINATION include)

