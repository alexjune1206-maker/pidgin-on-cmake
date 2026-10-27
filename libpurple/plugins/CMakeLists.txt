cmake_minimum_required(VERSION 3.16)
set(PLUGIN_SOURCES
    autoaccept.c
    buddynote.c
    codeinline.c
    dbus-example.c
    debug_example.c
    filectl.c
    helloworld.c
    idle.c
    joinpart.c
    log_reader.c
    newline.c
    notify_example.c
    offlinemsg.c
    one_time_password.c
    pluginpref_example.c
    psychic.c
    simple.c
    statenotify.c
)
# Build standalone base plugins if found
foreach(SRC ${PLUGIN_SOURCES})
    get_filename_component(PLUG_NAME ${SRC} NAME_WE)
    add_library(${PLUG_NAME} MODULE ${SRC})
    target_compile_definitions(${PLUG_NAME} PRIVATE -DPURPLE_PART_OF_CORE)
    target_include_directories(${PLUG_NAME} PRIVATE ${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} ${CMAKE_SOURCE_DIR}/libpurple)
    target_link_libraries(${PLUG_NAME} PRIVATE purple ${GLIB_LIBRARIES})
endforeach()
