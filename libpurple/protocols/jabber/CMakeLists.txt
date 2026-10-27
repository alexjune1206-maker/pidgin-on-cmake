# ==============================================================================
# PURPLE PROTOCOL - JABBER Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(JABBER_SOURCES
    adhoccommands.c
    auth.c
    auth_cyrus.c
    auth_digest_md5.c
    auth_plain.c
    auth_scram.c
    bosh.c
    buddy.c
    caps.c
    chat.c
    data.c
    disco.c
    ibb.c
    iq.c
    jabber.c
    jutil.c
    libxmpp.c
    message.c
    oob.c
    parser.c
    pep.c
    ping.c
    presence.c
    roster.c
    si.c
    stream_management.c
    useravatar.c
    usermood.c
    usernick.c
    usertune.c
    xdata.c
)

add_library(purple-jabber MODULE ${JABBER_SOURCES})
target_compile_definitions(purple-jabber PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-jabber PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-jabber PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-jabber DESTINATION lib/purple-2)
