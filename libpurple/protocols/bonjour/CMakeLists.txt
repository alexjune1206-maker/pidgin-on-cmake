# ==============================================================================
# PURPLE PROTOCOL - BONJOUR Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(BONJOUR_SOURCES
    bonjour.c
    bonjour_ft.c
    buddy.c
    dns_sd_proxy.c
    jabber.c
    mdns_avahi.c
    mdns_common.c
    mdns_dns_sd.c
    parser.c
)

add_library(purple-bonjour MODULE ${BONJOUR_SOURCES})
target_compile_definitions(purple-bonjour PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-bonjour PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-bonjour PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-bonjour DESTINATION lib/purple-2)
