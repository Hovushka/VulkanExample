project (Hova's_Engine)
cmake_minimum_required (VERSION 3.10)

set (CMAKE_CXX_STANDARD 20)

if (UNIX AND NOT APPLE)
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -g -ldl" )
    find_package (OpenMP REQUIRED)
else ()
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -g" )
endif ()

find_package (glfw3 3.3 REQUIRED)
find_package (glm REQUIRED)

include_directories (src external external/imgui external/volk)

add_executable (engine src/main.cpp
    external/volk/volk.c
    external/imgui/imgui.cpp 
    external/imgui/imgui_draw.cpp
    external/imgui/imgui_widgets.cpp
    external/imgui/imgui_demo.cpp
    external/imgui/imgui_impl_glfw.cpp
    external/imgui/imgui_impl_vulkan.cpp)

target_link_libraries (engine glfw)
# If doesn't link try this:
# target_link_libraries (engine glfw -ldl)

file (COPY models/ DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/models)
file (COPY textures/ DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/textures)
