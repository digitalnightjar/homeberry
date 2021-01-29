cmake_minimum_required(VERSION 3.13)

project(pimonitor
        VERSION 0.1
        DESCRIPTION "Homeberry Pimonitor,Library that provides system resource information for our PI Host."
        LANGUAGES CXX)

add_library(pimonitor main.cpp)