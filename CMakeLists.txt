cmake_minimum_required(VERSION 3.10)
project(cmake_planning_test2)
set(CMAKE_CXX_STANDARD 11)

#set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)#设置exe文件输出路径
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)#设置动态库和exe文件输出路径
#设置静态库，使用CMAKE_ARCHIVE_OUTPUT_DIRECTORY

aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LIST)#添加所有源文件到SRC_LIST变量中
#添加目标1
add_library(common SHARED ${SRC_LIST})#给所有源文件编译成一个动态库，名字为common
target_include_directories(common PUBLIC ${PROJECT_SOURCE_DIR}/include)#common动态库的链接头文件


#可执行文件生成，并且连接头文件，链接动态库，名字为planning_main，项目名为cmake_planning_test2
#添加目标2
add_executable(planning_main planning_main.cpp)
target_include_directories(planning_main PUBLIC ${PROJECT_SOURCE_DIR}/include)
target_link_libraries(planning_main PUBLIC common)
