cmake_minimum_required(VERSION 3.22 FATAL_ERROR)

project(
    "FirstProjectInCMake"
    VERSION 1.2.0
    DESCRIPTION "CMake C Project template for Operative Systems II"
    LANGUAGES C
    #AUTHOR "Landaeta Ezequiel Matias"
)

# Enable testing and add the tests 
include(CTest)

set(CMAKE_C_STANDARD 17)

include_directories(include)

# Include the include directory, where the header files are located
include(FetchContent)

# In this example we are going to use Unity to download the library from the git repository
set(UNITY_GIT_URL "https://github.com/ThrowTheSwitch/Unity.git")

set(FETCHCONTENT_QUIET OFF)

FetchContent_Declare(
    unity
    GIT_REPOSITORY ${UNITY_GIT_URL}
    SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/external/Unity
    UPDATE_COMMAND "" 
)

FetchContent_MakeAvailable(Unity)

file(GLOB_RECURSE SOURCES "src/*.c")

add_executable(${PROJECT_NAME} ${SOURCES})

add_subdirectory(lib/libdyn)
add_subdirectory(lib/libsta)

target_include_directories(${PROJECT_NAME} PUBLIC lib/libdyn/include)
target_include_directories(${PROJECT_NAME} PUBLIC lib/libsta/include)

target_link_libraries(${PROJECT_NAME} DynamiCLib StatiCLib)

if(RUN_TESTS EQUAL 1 OR RUN_COVERAGE EQUAL 1)
    add_subdirectory(tests)
endif()