cmake_minimum_required(VERSION 3.16)
set(PIDGIN_PLUGIN_SOURCES
    contact_priority.c
    convcolors.c
    extplacement.c
    gtkbuddynote.c
    history.c
    iconaway.c
    mailchk.c
    markerline.c
    notify.c
    pidgininc.c
    pidginrc.c
    raw.c
    relnot.c
    sendbutton.c
    spellchk.c
    themeedit.c
    themeedit-icon.c
    timestamp.c
    timestamp_format.c
    transparency.c
    unity.c
    vvconfig.c
    xmppconsole.c
)
foreach(SRC ${PIDGIN_PLUGIN_SOURCES})
    get_filename_component(PLUG_NAME ${SRC} NAME_WE)
    add_library(pidgin-${PLUG_NAME} MODULE ${SRC})
    target_include_directories(pidgin-${PLUG_NAME} PRIVATE ${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} ${CMAKE_SOURCE_DIR}/libpurple ${CMAKE_SOURCE_DIR}/pidgin)
    target_link_libraries(pidgin-${PLUG_NAME} PRIVATE purple pidgin ${GLIB_LIBRARIES} ${GTK_LIBRARIES})
endforeach()
