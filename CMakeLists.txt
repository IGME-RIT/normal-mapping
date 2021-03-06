
if(WIN32)
cmake_minimum_required (VERSION 3.1)
else()
cmake_minimum_required (VERSION 3.0)
endif()

project(normal-mapping-tutorial)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

set (normal-mapping-tutorial_VERSION_MAJOR 1)
set (normal-mapping-tutorial_VERSION_MINOR 0)
set (normal-mapping-tutorial_VERSION_BUILD 0)

file(
    COPY ${CMAKE_SOURCE_DIR}/src/main.cpp
    DESTINATION ${CMAKE_BINARY_DIR}
)

add_executable(normal-mapping-tutorial ${CMAKE_BINARY_DIR}/main.cpp)

if (MSVC)
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/glew-1.13.0-win32.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/glew-1.13.0-win32.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/glfw-3.1.2.bin.WIN32.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/glfw-3.1.2.bin.WIN32.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/glm-0.9.7.1.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/glm-0.9.7.1.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )
    file(
        COPY ${CMAKE_SOURCE_DIR}/lib/FreeImage3170Win32Win64.zip
        DESTINATION ${CMAKE_BINARY_DIR}
    )
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E tar xfz ${CMAKE_BINARY_DIR}/FreeImage3170Win32Win64.zip
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}
    )

    target_link_libraries(normal-mapping-tutorial
      ${CMAKE_BINARY_DIR}/glew-1.13.0/lib/Release/Win32/glew32.lib
      ${CMAKE_BINARY_DIR}/glfw-3.1.2.bin.WIN32/lib-vc2015/glfw3.lib
      ${CMAKE_BINARY_DIR}/FreeImage/Dist/x32/FreeImage.lib
      opengl32.lib
    )

    include_directories(
        ${CMAKE_BINARY_DIR}/glew-1.13.0/include
        ${CMAKE_BINARY_DIR}/glfw-3.1.2.bin.WIN32/include
        ${CMAKE_BINARY_DIR}/glm
        ${CMAKE_BINARY_DIR}/FreeImage/Dist/x32
    )

    add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_BINARY_DIR}/glew-1.13.0/bin/Release/Win32/glew32.dll"      # <--this is in-file
            $<TARGET_FILE_DIR:normal-mapping-tutorial>)

    add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/VertexShader.glsl"      # <--this is in-file
            $<TARGET_FILE_DIR:normal-mapping-tutorial>)

    add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/FragmentShader.glsl"      # <--this is in-file
            $<TARGET_FILE_DIR:normal-mapping-tutorial>)

    add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/VertexShader.glsl"      # <--this is in-file
            ${CMAKE_BINARY_DIR})

    add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_SOURCE_DIR}/src/FragmentShader.glsl"      # <--this is in-file
            ${CMAKE_BINARY_DIR})

    add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
            "${CMAKE_BINARY_DIR}/FreeImage/Dist/x32/FreeImage.dll"
            $<TARGET_FILE_DIR:normal-mapping-tutorial>)
endif (MSVC)

add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/brickNorm.png"
        $<TARGET_FILE_DIR:normal-mapping-tutorial>)
add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/brickNorm.png"
        ${CMAKE_BINARY_DIR})
add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/brickTexture.png"
        $<TARGET_FILE_DIR:normal-mapping-tutorial>)
add_custom_command(TARGET normal-mapping-tutorial POST_BUILD        # Adds a post-build event to MyTest
    COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
    	"${CMAKE_SOURCE_DIR}/assets/brickTexture.png"
        ${CMAKE_BINARY_DIR})
# vim: ts=4 sw=4 et
