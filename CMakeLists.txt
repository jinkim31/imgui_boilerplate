cmake_minimum_required(VERSION 3.0)
project(imgui_boilerplate)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_COMMON
        src/main.cpp
        # imgui
        lib/imgui/imgui.cpp
        lib/imgui/imgui_widgets.cpp
        lib/imgui/imgui_tables.cpp
        lib/imgui/imgui_demo.cpp
        lib/imgui/imgui_draw.cpp
        # implot
        lib/implot/implot.cpp
        lib/implot/implot_items.cpp
        lib/implot/implot_demo.cpp
)

if(UNIX)
        add_executable(imgui_boilerplate
                ${SRC_COMMON}
                lib/imgui/backends/imgui_impl_glut.cpp
                lib/imgui/backends/imgui_impl_opengl2.cpp
        )

        target_link_libraries(imgui_boilerplate
                glut
                GL
        )
elseif(APPLE)
        add_executable(imgui_boilerplate
                ${SRC_COMMON}
                lib/imgui/backends/imgui_impl_metal.mm
                lib/imgui/backends/imgui_impl_glfw.cpp
        )

        target_link_libraries(imgui_boilerplate
                "-framework Metal"
                "-framework MetalKit"
                "-framework AppKit"
                "-framework Foundation"
                "-framework QuartzCore"
                "glfw"
        )
endif()

target_include_directories(imgui_boilerplate PUBLIC
        lib/imgui
        lib/imgui/backends
        lib/implot
)
