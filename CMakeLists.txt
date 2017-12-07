cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_STANDARD 11)

include(cmake/HunterGate.cmake)

HunterGate(
    URL "https://github.com/poljkee2010/hunter/archive/v0.19.137.1.tar.gz"
    SHA1 "c85118ae943500d5fce2afb24cee4253eb3296ae"
)

project(demo)

hunter_add_package(print)
find_package(print)
hunter_add_package(Boost COMPONENTS system filesystem program_options)
find_package(Boost REQUIRED system filesystem program_options)

add_executable(demo ${CMAKE_CURRENT_SOURCE_DIR}/sources/demo.cpp) # Создаём исполняемый файл demo по исходному файлу demo.cpp
target_link_libraries(demo print Boost::system Boost::filesystem Boost::program_options) # линковка цели demo с целью print и целями filesystem,system,program_options из пространства имён Boost 

install(TARGETS demo RUNTIME DESTINATION bin)
