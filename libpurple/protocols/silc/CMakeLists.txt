# ==============================================================================
# PURPLE PROTOCOL - SILC Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(SILC_SOURCES
    buddy.c
    chat.c
    ft.c
    ops.c
    pk.c
    silc.c
    util.c
    wb.c
)

add_library(purple-silc MODULE ${SILC_SOURCES})
target_compile_definitions(purple-silc PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-silc PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-silc PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-silc DESTINATION lib/purple-2)
