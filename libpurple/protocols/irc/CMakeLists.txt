# ==============================================================================
# PURPLE PROTOCOL - IRC Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(IRC_SOURCES
    cmds.c
    dcc_send.c
    irc.c
    msgs.c
    parse.c
)

add_library(purple-irc MODULE ${IRC_SOURCES})
target_compile_definitions(purple-irc PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-irc PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-irc PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-irc DESTINATION lib/purple-2)
