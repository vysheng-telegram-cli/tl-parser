cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(tl-parser LANGUAGES C)

set(SRCS
	src/crc32.c
	src/tl-parser.c
	src/tlc.c)
if (WIN32)
list(APPEND SOURCES wgetopt.c wgetopt.h)
endif()

add_executable(${PROJECT_NAME} ${SRCS})
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include/tl_parser)

if (NOT WIN32)
target_link_libraries(${PROJECT_NAME} m)
else()
add_definitions("-D_CRT_SECURE_NO_WARNINGS")
if (MSVC)
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /utf-8")
endif()
endif()

