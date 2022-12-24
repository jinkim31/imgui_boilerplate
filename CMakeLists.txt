cmake_minimum_required(VERSION 3.0)
project(imgui_boilerplate)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(GLOB IMGUI_SRC
        "imgui/*.cpp"
        imgui/backends/imgui_impl_metal.mm
        imgui/backends/imgui_impl_glfw.cpp
)

add_library(imgui_lib STATIC
    ${IMGUI_SRC}
)

target_include_directories(imgui_lib PUBLIC
        imgui
        imgui/backends
)

target_link_libraries(imgui_lib
        "-framework Metal"
        "-framework MetalKit"
        "-framework AppKit"
        "-framework Foundation"
        "-framework QuartzCore"
        "glfw"
        )

add_executable(imgui_boilerplate
        src/main.mm)

target_link_libraries(imgui_boilerplate
        imgui_lib
)
