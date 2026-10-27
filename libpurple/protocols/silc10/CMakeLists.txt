# ==============================================================================
# PURPLE PROTOCOL - SILC10 Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(SILC10_SOURCES
    buddy.c
    chat.c
    ft.c
    ops.c
    pk.c
    silc.c
    util.c
    wb.c
)

add_library(purple-silc10 MODULE ${SILC10_SOURCES})
target_compile_definitions(purple-silc10 PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-silc10 PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-silc10 PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-silc10 DESTINATION lib/purple-2)
