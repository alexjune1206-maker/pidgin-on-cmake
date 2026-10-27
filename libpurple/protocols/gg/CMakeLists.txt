# ==============================================================================
# PURPLE PROTOCOL - GG Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(GG_SOURCES
    buddylist.c
    confer.c
    gg.c
    gg-utils.c
    search.c
)

add_library(purple-gg MODULE ${GG_SOURCES})
target_compile_definitions(purple-gg PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-gg PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-gg PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-gg DESTINATION lib/purple-2)
