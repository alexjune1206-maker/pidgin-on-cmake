# ==============================================================================
# PURPLE PROTOCOL - SAMETIME Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(SAMETIME_SOURCES
    sametime.c
)

add_library(purple-sametime MODULE ${SAMETIME_SOURCES})
target_compile_definitions(purple-sametime PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-sametime PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-sametime PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-sametime DESTINATION lib/purple-2)
