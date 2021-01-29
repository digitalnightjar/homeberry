cmake_minimum_required(VERSION 3.13)

project(auth
        VERSION 0.1
        DESCRIPTION "Homeberry auth, provider of basic user authentication."
        LANGUAGES CXX)

add_executable(auth main.cpp)