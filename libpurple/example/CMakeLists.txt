# ==============================================================================
# PURPLE EXAMPLES - Client Implementation Examples
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/nullclient.c")
    add_executable(nullclient nullclient.c)
    target_include_directories(nullclient PRIVATE
        ${CMAKE_SOURCE_DIR}
        ${CMAKE_BINARY_DIR}
        ${CMAKE_SOURCE_DIR}/libpurple
    )
    target_link_libraries(nullclient PRIVATE purple ${GLIB_LIBRARIES})
endif()
