#
# Copyright (c) 2014-2016 Alex Spataru <alex_spataru@outlook.com>
#
# This file is part of the QSimpleUpdater library, which is released under
# the DBAD license, you can read a copy of it below:
#
# DON'T BE A DICK PUBLIC LICENSE TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION
# AND MODIFICATION:
#
# Do whatever you like with the original work, just don't be a dick.
# Being a dick includes - but is not limited to - the following instances:
#
# 1a. Outright copyright infringement - Don't just copy this and change the
#     name.
# 1b. Selling the unmodified original with no work done what-so-ever, that's
#     REALLY being a dick.
# 1c. Modifying the original work to contain hidden harmful content.
#     That would make you a PROPER dick.
#
# If you become rich through modifications, related works/services, or
# supporting the original work, share the love.
# Only a dick would make loads off this work and not buy the original works
# creator(s) a pint.
#
# Code is provided with no warranty. Using somebody else's code and bitching
# when it goes wrong makes you a DONKEY dick.
# Fix the problem yourself. A non-dick would submit the fix back.

cmake_minimum_required(VERSION 3.10)

project(qsimpleupdater)

#set(CMAKE_CXX_STANDARD 17)

# Instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)
# Create code from a list of Qt designer ui files
set(CMAKE_AUTOUIC ON)
# Resource compiler
set(CMAKE_AUTORCC ON)

# FIXME do we need this?
#remove_definitions(-DQT_NO_KEYWORDS)

#add_definitions(-DQT_NO_KEYWORDS)

add_library(${PROJECT_NAME}
    etc/resources/qsimpleupdater.qrc
    src/Downloader.ui
    src/Updater.h
    src/Downloader.h
    src/Updater.cpp
    src/Downloader.cpp
    src/QSimpleUpdater.cpp
    include/QSimpleUpdater.h
)
set(CMAKE_VERBOSE_MAKEFILE ON)

# for the SingleApplication class
set(QAPPLICATION_CLASS QApplication CACHE STRING "Inheritance class for SingleApplication")

include_directories(
    .
    src/
    include/
)

find_package(Qt5Gui CONFIG REQUIRED)
find_package(Qt5Core CONFIG REQUIRED)
find_package(Qt5Network CONFIG REQUIRED)
find_package(Qt5Widgets CONFIG REQUIRED)

include_directories(${Qt5Widgets_INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME} ${Qt5Gui_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${Qt5Core_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${Qt5Network_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${Qt5Widgets_LIBRARIES})

# FIXME this might cause problems - qknight
#if (UNIX)
#    target_compile_options(${PROJECT_NAME} PRIVATE -Werror -Wall -Wextra -Werror=return-type
#            -Wno-unknown-pragmas -Wno-unused-parameter -Wno-sign-compare -Wno-reorder -Wno-unused-variable
#            -Wno-unused-but-set-variable)
#endif ()
