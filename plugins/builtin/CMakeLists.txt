cmake_minimum_required(VERSION 3.16)
# Change this to the name of your plugin #
project(builtin)

# Add your source files here #
add_library(${PROJECT_NAME} SHARED
        source/plugin_builtin.cpp

        source/content/command_palette_commands.cpp
        source/content/data_inspector.cpp
        source/content/pl_builtin_functions.cpp
        source/content/settings_entries.cpp
        source/content/tools_entries.cpp
        source/content/data_processor_nodes.cpp
        source/content/ui_items.cpp
        source/content/providers.cpp
        source/content/views.cpp

        source/content/providers/file_provider.cpp
        source/content/providers/gdb_provider.cpp
        source/content/providers/disk_provider.cpp

        source/content/views/view_hexeditor.cpp
        source/content/views/view_pattern_editor.cpp
        source/content/views/view_pattern_data.cpp
        source/content/views/view_hashes.cpp
        source/content/views/view_information.cpp
        source/content/views/view_help.cpp
        source/content/views/view_tools.cpp
        source/content/views/view_strings.cpp
        source/content/views/view_data_inspector.cpp
        source/content/views/view_disassembler.cpp
        source/content/views/view_bookmarks.cpp
        source/content/views/view_patches.cpp
        source/content/views/view_command_palette.cpp
        source/content/views/view_settings.cpp
        source/content/views/view_data_processor.cpp
        source/content/views/view_yara.cpp
        source/content/views/view_constants.cpp
        source/content/views/view_store.cpp
        source/content/views/view_diff.cpp
        source/content/views/view_provider_settings.cpp


        source/math_evaluator.cpp

        source/lang/en_US.cpp
        source/lang/de_DE.cpp
        source/lang/it_IT.cpp
        source/lang/zh_CN.cpp
)

# Add additional include directories here #
target_include_directories(${PROJECT_NAME} PRIVATE include)

# Add additional libraries here #
target_link_libraries(${PROJECT_NAME} PRIVATE libimhex LLVMDemangle)

# ---- No need to change anything from here downwards unless you know what you're doing ---- #

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_SHARED_LIBRARY_PREFIX "")
set(CMAKE_SHARED_LIBRARY_SUFFIX ".hexplug")

if (WIN32)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wl,--allow-multiple-definition -fvisibility=hidden")
endif()

add_compile_definitions(IMHEX_PLUGIN_NAME=${PROJECT_NAME})
set_target_properties(${PROJECT_NAME} PROPERTIES POSITION_INDEPENDENT_CODE ON)

if (NOT TARGET libimhex)
    add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../libimhex ${CMAKE_CURRENT_BINARY_DIR}/plugins/libimhex)
endif()