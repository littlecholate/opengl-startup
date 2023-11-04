cmake_minimum_required(VERSION 3.16)
set(CMAKE_CXX_STANDARD 11)

# disable GLFW docs, examples and tests
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)

project(opengl-startup)

add_executable("${CMAKE_PROJECT_NAME}")

# update all the submodules
find_package(GIT QUIET)
if(GIT_FOUND AND EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/.git")
    option(GIT_SUBMODULE "Check submodules during build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                        RESULT_VARIABLE GIT_SUBMODULE_RESULT)
        if(NOT GIT_SUBMODULE_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMODULE_RESULT}")
        endif()
    endif()
endif()

# add path to subdirectory CMakeLists
add_subdirectory(external/glfw) # window oppener
add_subdirectory(external/glad) # opengl loader

# get the source files path
# define MY_SOURCES to be a list of all the source files 
file(GLOB_RECURSE MY_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
target_sources("${CMAKE_PROJECT_NAME}" PRIVATE ${MY_SOURCES})

# get the assets path, uncomment second line for release version
# see the https://www.youtube.com/watch?v=A735Y4kMIPM
target_compile_definitions("${CMAKE_PROJECT_NAME}" PUBLIC RESOURCES_PATH="${CMAKE_CURRENT_SOURCE_DIR}/res/") 
#target_compile_definitions("${CMAKE_PROJECT_NAME}" PUBLIC RESOURCES_PATH="./resources/") 

# get the .h files path
# target_include_directories("${CMAKE_PROJECT_NAME}" PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/src/Engine/")

target_link_libraries("${CMAKE_PROJECT_NAME}" PRIVATE glfw glad)