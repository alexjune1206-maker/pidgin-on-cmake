# ==============================================================================
# PURPLE PROTOCOL - NULL Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(NULL_SOURCES
    nullprpl.c
)

add_library(purple-null MODULE ${NULL_SOURCES})
target_compile_definitions(purple-null PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-null PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-null PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-null DESTINATION lib/purple-2)
