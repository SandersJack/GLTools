cmake_minimum_required(VERSION 3.2)

project(GLTools)

file(GLOB SOURCES src/*.cc)
include_directories(include)
# Add your source files
add_library(GLTools STATIC ${SOURCES})

# Include directory for header files
target_include_directories(GLTools PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
# Add the source and include directories
add_subdirectory(MathGL)

# Include directory for header files
include_directories(MathGL/include)
target_link_libraries(GLTools PRIVATE MathGL)

add_subdirectory(Controls)

# Include directory for header files
include_directories(Controls/include)
target_link_libraries(GLTools PRIVATE Controls)

find_package(OpenGL REQUIRED OpenGL)

find_package(GLEW REQUIRED)

target_include_directories(${PROJECT_NAME} PRIVATE ${GLFW_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PRIVATE OpenGL::OpenGL GLEW::GLEW ${GLFW_LIBRARIES})

find_package(Freetype REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE Freetype::Freetype)