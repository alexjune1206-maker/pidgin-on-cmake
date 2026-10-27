cmake_minimum_required(VERSION 3.16)
set(CIPHER_SOURCES
    des.c
    gchecksum.c
    hmac.c
    md4.c
    md5.c
    rc4.c
    sha1.c
    sha256.c
)
add_library(purple-ciphers STATIC ${CIPHER_SOURCES})
target_compile_definitions(purple-ciphers PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-ciphers PRIVATE ${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR} ${CMAKE_SOURCE_DIR}/libpurple)
target_link_libraries(purple-ciphers PRIVATE ${GLIB_LIBRARIES})
