
cmake_minimum_required(VERSION 3.7)
project(arduboy-emulator)

file(GLOB_RECURSE SRCS "src/*.c" "src/*.h")

set(CMAKE_SUPPRESS_REGENERATION true)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/lib)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_CURRENT_LIST_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_LIST_DIR}/bin)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

find_package(SDL2 REQUIRED)
find_package(OpenGL REQUIRED)

include_directories(simavr/simavr/cores
					simavr/simavr/sim
					/usr/local/include
					${SDL2_INCLUDE_DIRS})

add_subdirectory(simavr)

# The library itself
add_executable(arduboy-emulator ${SRCS})

target_link_libraries(arduboy-emulator 
					  simavr 
					  ${SDL2_LIBRARIES} 
					  ${OPENGL_LIBRARIES})
