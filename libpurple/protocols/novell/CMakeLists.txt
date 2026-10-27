# ==============================================================================
# PURPLE PROTOCOL - NOVELL Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(NOVELL_SOURCES
    nmconference.c
    nmconn.c
    nmcontact.c
    nmevent.c
    nmfield.c
    nmmessage.c
    nmrequest.c
    nmrtf.c
    nmuser.c
    nmuserrecord.c
    novell.c
)

add_library(purple-novell MODULE ${NOVELL_SOURCES})
target_compile_definitions(purple-novell PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-novell PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-novell PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-novell DESTINATION lib/purple-2)
