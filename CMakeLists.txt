cmake_minimum_required(VERSION 3.20)

project(dicom_search LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(${PROJECT_NAME}
    src/main.cpp

)

target_include_directories(${PROJECT_NAME} PRIVATE include)

find_package(SQLite3 REQUIRED)     # target: SQLite::SQLite3
find_package(DCMTK   REQUIRED)     # target: dcmtk::dcmtk

target_link_libraries(${PROJECT_NAME}
    PRIVATE
        SQLite::SQLite3
        dcmtk::dcmtk
)

if(MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE /W4)
else()
    target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Wpedantic)
endif()

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
