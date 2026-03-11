cmake_minimum_required(VERSION 3.20)

project(Eclosion LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

file(GLOB_RECURSE APP_SOURCES CONFIGURE_DEPENDS
    "${CMAKE_SOURCE_DIR}/source/*.cpp"
)

file(GLOB_RECURSE APP_HEADERS CONFIGURE_DEPENDS
    "${CMAKE_SOURCE_DIR}/source/*.hpp"
    "${CMAKE_SOURCE_DIR}/source/*.h"
)

add_subdirectory(vendored/SDL EXCLUDE_FROM_ALL)

add_executable(${PROJECT_NAME}
    "${CMAKE_SOURCE_DIR}/main.cpp"
    ${APP_SOURCES}
    ${APP_HEADERS}
)

target_include_directories(${PROJECT_NAME} PRIVATE
    "${CMAKE_SOURCE_DIR}"
    "${CMAKE_SOURCE_DIR}/source"
)

target_link_libraries(${PROJECT_NAME} PRIVATE SDL3::SDL3)