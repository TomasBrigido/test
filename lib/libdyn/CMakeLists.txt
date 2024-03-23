# Request the minimum version of CMake, in case of lower version throws error.
cmake_minimum_required(VERSION 3.22 FATAL_ERROR)

#Define project
project(
    "DynamiCLib"
    VERSION 1.0.0
    DESCRIPTION "CMake C Project Template for Operating Sistem II"
    LANGUAGES C
)

#Define the C standar, we are going to use std17
set(CMAKE_C_STANDARD 17)

#Include the 'include' directory, where the headers are located
include_directories(include)

#Add the 'src' directory, where the source files are located
file(GLOB_RECURSE SOURCES "src/*.c")

#Create the executable
add_library(${PROJECT_NAME} SHARED ${SOURCES})

