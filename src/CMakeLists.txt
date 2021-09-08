cmake_minimum_required(VERSION 3.5)

project(qt-cef LANGUAGES CXX)

# CMAKE_PREFIX_PATH 实际值为本地安装的QT中的对应编译环境的目录
set(CMAKE_PREFIX_PATH "D:\\Programs\\Qt\\Qt5.14.2\\5.14.2\\msvc2017_64")
# 一个基于QT Widget的项目，以下的两个路径是必备的
set(Qt5_DIR "${CMAKE_PREFIX_PATH}/lib/cmake/Qt5")
set(Qt5Widgets_DIR "${CMAKE_PREFIX_PATH}/lib/cmake/Qt5Widgets")
# 配置了上述后，可以通过find_package来搜索对应的cmake文件

set(CMAKE_INCLUDE_CURRENT_DIR ON)

# UIC、MOC、RCC启用
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt5 COMPONENTS Widgets REQUIRED)

# 添加所有的文件：
# 头文件、源文件、QT ui文件、QT qrc资源文件
# 特别的，在Windows下VS下，还需要manifest文件，并且该文件在cmake3.4以后就能够自动是被并被引入
add_executable(qt-cef
qtcefwindow.h
simple_app.h
simple_handler.h
stdafx.h
main.cpp
qtcefwindow.cpp
simple_app.cpp
simple_handler.cpp
stdafx.cpp
qtcefwindow.ui
qtcefwindow.qrc
app.manifest
)

# CEF相关头文件的引入
include_directories("${CMAKE_SOURCE_DIR}/CefFiles")
include_directories("${CMAKE_SOURCE_DIR}/CefFiles/include")

# 动、静态库连接
target_link_libraries(qt-cef
PRIVATE Qt5::Widgets 
"${CMAKE_SOURCE_DIR}/CefFiles/bin/Debug/libcef.lib"
"${CMAKE_SOURCE_DIR}/CefFiles/bin/Debug/libcef_dll_wrapper.lib"
)
