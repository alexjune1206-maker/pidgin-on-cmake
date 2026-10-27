# ==============================================================================
# PURPLE PROTOCOL - ZEPHYR Module Build Map
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

set(ZEPHYR_SOURCES
    error_message.c
    et_name.c
    init_et.c
    ZAsyncLocate.c
    ZCkAuth.c
    ZCkIfNot.c
    ZClosePort.c
    ZCmpUID.c
    ZCmpUIDP.c
    zephyr.c
    zephyr_err.c
    ZFlsLocs.c
    ZFlsSubs.c
    ZFmtAuth.c
    ZFmtList.c
    ZFmtNotice.c
    ZFmtRaw.c
    ZFmtRawLst.c
    ZFmtSmRaw.c
    ZFmtSmRLst.c
    ZFreeNot.c
    ZGetLocs.c
    ZGetSender.c
    ZGetSubs.c
    ZGetWGPort.c
    ZhmStat.c
    ZIfNotice.c
    ZInit.c
    Zinternal.c
    ZLocations.c
    ZMakeAscii.c
    ZMkAuth.c
    ZNewLocU.c
    ZOpenPort.c
    ZParseNot.c
    ZPeekIfNot.c
    ZPeekNot.c
    ZPeekPkt.c
    ZPending.c
    ZReadAscii.c
    ZRecvNot.c
    ZRecvPkt.c
    ZRetSubs.c
    ZSendList.c
    ZSendNot.c
    ZSendPkt.c
    ZSendRaw.c
    ZSendRLst.c
    ZSetDest.c
    ZSetFD.c
    ZSetSrv.c
    ZSubs.c
    ZVariables.c
    ZWait4Not.c
)

add_library(purple-zephyr MODULE ${ZEPHYR_SOURCES})
target_compile_definitions(purple-zephyr PRIVATE -DPURPLE_PART_OF_CORE)
target_include_directories(purple-zephyr PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
    ${CMAKE_SOURCE_DIR}/libpurple
    ${CMAKE_CURRENT_SOURCE_DIR}
)
target_link_libraries(purple-zephyr PRIVATE purple ${GLIB_LIBRARIES} ${LIBXML_LIBRARIES})
install(TARGETS purple-zephyr DESTINATION lib/purple-2)
