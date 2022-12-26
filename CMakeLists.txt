cmake_minimum_required(VERSION 3.0)
project(imgui_boilerplate)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# imgui library

file(GLOB IMGUI_SRC
        "imgui/*.cpp"
        imgui/backends/imgui_impl_metal.mm
        imgui/backends/imgui_impl_glfw.cpp
)

add_library(imgui STATIC
    ${IMGUI_SRC}
)

target_include_directories(imgui PUBLIC
        imgui
        imgui/backends
)

target_link_libraries(imgui
        "-framework Metal"
        "-framework MetalKit"
        "-framework AppKit"
        "-framework Foundation"
        "-framework QuartzCore"
        "glfw"
        )

# implot library

add_library(implot STATIC
        implot/implot.cpp
        implot/implot_items.cpp
        implot/implot_demo.cpp
        )

target_include_directories(implot PUBLIC
        implot)

target_link_libraries(implot
        imgui)

# main executable
add_executable(imgui_boilerplate
        src/main.mm)

target_link_libraries(imgui_boilerplate
        imgui
        implot
)

target_include_directories(imgui_boilerplate PRIVATE
        IconFontCppHeaders
        )