cmake_minimum_required(VERSION 3.0)
project(imgui_boilerplate)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(EXECUTABLE_NAME app)

set(SRC_COMMON
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
        # user
        src/custom_widgets.cpp
        src/application.cpp
)

if(APPLE)
        add_executable(${EXECUTABLE_NAME}
                src/main_glfw_metal.mm
                ${SRC_COMMON}
                lib/imgui/backends/imgui_impl_glfw.cpp
                lib/imgui/backends/imgui_impl_metal.mm
        )
        target_link_libraries(${EXECUTABLE_NAME}
                "-framework Metal"
                "-framework MetalKit"
                "-framework AppKit"
                "-framework Foundation"
                "-framework QuartzCore"
                "glfw"
        )
elseif(UNIX)
        add_executable(${EXECUTABLE_NAME}
                src/main_glwf_opengl2.cpp
                ${SRC_COMMON}
                lib/imgui/backends/imgui_impl_glut.cpp
                lib/imgui/backends/imgui_impl_opengl2.cpp
        )
        target_link_libraries(${EXECUTABLE_NAME}
                glut
                GL
        )
else()
        find_package(FreeGLUT REQUIRED PATHS "C:/msys64/mingw64/bin")
        find_library(glfw3 NAMES glwf3 libglfw3 PATHS "C:/GLFW/lib-mingw-w64" REQUIRED)
        add_executable(${EXECUTABLE_NAME}
                src/main_glwf_opengl2.cpp
                ${SRC_COMMON}
                lib/imgui/backends/imgui_impl_opengl2.cpp
                lib/imgui/backends/imgui_impl_glfw.cpp
                )
        target_include_directories(${EXECUTABLE_NAME} PRIVATE "C:/GLFW/include")
        target_link_libraries(${EXECUTABLE_NAME}
                FreeGLUT::freeglut
                ${glfw3}
        )
endif()

target_include_directories(${EXECUTABLE_NAME} PUBLIC
        lib/imgui
        lib/imgui/backends
        lib/implot
)