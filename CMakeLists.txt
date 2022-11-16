cmake_minimum_required(VERSION 3.24)
project(pipewire_video_src C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_FLAGS "-lm")

find_package(PkgConfig REQUIRED)
pkg_check_modules(PIPEWIRE REQUIRED libpipewire-0.3)

find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

add_executable(pipewire_basic pipewirebasic.cpp)
add_executable(pipewire_video_src pipewire-video-src.c)
add_executable(pipewire-video-play sdl.h pipewire-video-play.c)


target_link_libraries(pipewire_video_src ${PIPEWIRE_LIBRARIES})
target_include_directories(pipewire_video_src PUBLIC ${PIPEWIRE_INCLUDE_DIRS})
target_compile_options(pipewire_video_src PUBLIC ${PIPEWIRE_CFLAGS_OTHER})

target_link_libraries(pipewire_basic ${PIPEWIRE_LIBRARIES})
target_include_directories(pipewire_basic PUBLIC ${PIPEWIRE_INCLUDE_DIRS})
target_compile_options(pipewire_basic PUBLIC ${PIPEWIRE_CFLAGS_OTHER})

target_link_libraries(pipewire-video-play ${PIPEWIRE_LIBRARIES} ${SDL2_LIBRARIES})
target_include_directories(pipewire-video-play PUBLIC ${PIPEWIRE_INCLUDE_DIRS})
target_compile_options(pipewire-video-play PUBLIC ${PIPEWIRE_CFLAGS_OTHER})
