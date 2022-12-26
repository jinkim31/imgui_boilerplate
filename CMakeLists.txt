cmake_minimum_required(VERSION 3.0)
project(imgui_boilerplate)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SRC_COMMON
        src/main.cpp
        # imgui
        imgui/imgui.cpp
        imgui/imgui_widgets.cpp
        imgui/imgui_tables.cpp
        imgui/imgui_demo.cpp
        imgui/imgui_draw.cpp
        #implot
        implot/

)

if(UNIX)
        add_executable(imgui_boilerplate
                ${SRC_COMMON}
                imgui/backends/imgui_impl_glut.cpp
                imgui/backends/imgui_impl_opengl2.cpp
        )

        target_link_libraries(imgui_boilerplate
        glut
        GL
)
elseif(APPLE)
        add_executable(imgui_boilerplate
                ${SRC_COMMON}
                imgui/backends/imgui_impl_metal.mm
                imgui/backends/imgui_impl_glfw.cpp
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
        imgui
        imgui/backends
)
