cmake_minimum_required(VERSION 3.17)
project(dear-imgui-template)

set(CMAKE_CXX_STANDARD 20)
set(LIBRARIES_DIR lib)

add_executable(dear-imgui-template
        vendor/imgui_impl_glfw.h
        vendor/imgui_impl_glfw.cpp
        vendor/imgui_impl_opengl3.h
        vendor/imgui_impl_opengl3.cpp
        src/main.cpp)

# glad
set(GLAD_DIR "${LIBRARIES_DIR}/glad")
add_library("glad" "${GLAD_DIR}/src/glad.c")
target_include_directories("glad" PRIVATE "${GLAD_DIR}/include")
target_include_directories(${PROJECT_NAME} PRIVATE "${GLAD_DIR}/include")
target_link_libraries(${PROJECT_NAME} "glad" "${CMAKE_DL_LIBS}")

# glfw
set(GLFW_DIR "${LIBRARIES_DIR}/glfw")
set(GLFW_BUILD_EXAMPLES OFF CACHE INTERNAL "Build the GLFW example programs")
set(GLFW_BUILD_TESTS OFF CACHE INTERNAL "Build the GLFW test programs")
set(GLFW_BUILD_DOCS OFF CACHE INTERNAL "Build the GLFW documentation")
set(GLFW_INSTALL OFF CACHE INTERNAL "Generate installation target")
add_subdirectory("${GLFW_DIR}")
target_link_libraries(${PROJECT_NAME} "glfw" "${GLFW_LIBRARIES}")
target_include_directories(${PROJECT_NAME} PRIVATE "${GLFW_DIR}/include")
target_compile_definitions(${PROJECT_NAME} PRIVATE "GLFW_INCLUDE_NONE")

# imgui
set(IMGUI_DIR "${LIBRARIES_DIR}/imgui")
add_library("imgui"
        "${IMGUI_DIR}/src/imgui.cpp"
        "${IMGUI_DIR}/src/imgui_draw.cpp"
        "${IMGUI_DIR}/src/imgui_demo.cpp"
        "${IMGUI_DIR}/src/imgui_widgets.cpp")
target_include_directories("imgui" PRIVATE "${IMGUI_DIR}/include")
target_include_directories(${PROJECT_NAME} PRIVATE "${IMGUI_DIR}/include")
target_link_libraries(${PROJECT_NAME} "imgui" "${CMAKE_DL_LIBS}")