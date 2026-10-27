# ==============================================================================
# PURPLE PROTOCOL - SIMPLE Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(SIMPLE_SOURCES
    simple.c
    sipmsg.c
)

add_library(purple-simple MODULE ${SIMPLE_SOURCES})
target_compile_definitions(purple-simple PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-simple PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-simple PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-simple DESTINATION lib/purple-2)
