cmake_minimum_required(VERSION 3.15)  # CMake version check
project(vertex-core)               # project name
set(CMAKE_CXX_STANDARD 17)            # enable c++17 standard
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(OpenGL REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(GLEW CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(freeimage CONFIG REQUIRED)
find_package(assimp CONFIG REQUIRED)
find_package(FreeGLUT CONFIG REQUIRED)

file(GLOB_RECURSE SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c"
)

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE
    "${CMAKE_CURRENT_SOURCE_DIR}/include"
    ${imgui_INCLUDE_DIRS}
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    glfw
    glm::glm
    imgui::imgui
    GLEW::GLEW
    FreeGLUT::freeglut          # use FreeGLUT::freeglut_static for static linking
    assimp::assimp
    freeimage::FreeImage
    OpenGL::GL
)


if(WIN32)
    target_compile_definitions(${PROJECT_NAME} PRIVATE WIN32_LEAN_AND_MEAN)
endif()