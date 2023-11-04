cmake_minimum_required(VERSION 3.1)

project(glad)

add_library(${PROJECT_NAME})

target_sources(${PROJECT_NAME} PRIVATE src/glad.c)
target_include_directories(${PROJECT_NAME} PUBLIC include)