# ==============================================================================
# PIDGIN - GTK+ Graphical User Interface Build Configuration
# ==============================================================================
cmake_minimum_required(VERSION 3.16)

# Collect all the GTK interface source files
set(PIDGIN_SOURCES
    gtkaccount.c
    gtkblist.c
    gtkblist-theme.c
    gtkblist-theme-loader.c
    gtkcertmgr.c
    gtkcellrendererexpander.c
    gtkcmime.c
    gtkconv.c
    gtkconv-theme.c
    gtkconv-theme-loader.c
    gtkdebug.c
    gtkdialogs.c
    gtkdnd-hints.c
    gtkeventloop.c
    gtkft.c
    gtkicon-theme.c
    gtkicon-theme-loader.c
    gtkidle.c
    gtkimhtml.c
    gtkimhtmltoolbar.c
    gtklog.c
    gtkmain.c
    gtkmedia.c
    gtkmenutray.c
    gtknotify.c
    gtkplugin.c
    gtkpluginpref.c
    gtkpounce.c
    gtkprefs.c
    gtkprivacy.c
    gtkrequest.c
    gtkroomlist.c
    gtksavedstatuses.c
    gtkscrollbook.c
    gtksound.c
    gtksourceiter.c
    gtksourceundomanager.c
    gtkstatus-lists.c
    gtkstatusbox.c
    gtkthemes.c
    gtkutils.c
    gtkwhiteboard.c
    pidginstock.c
)

# Collect main user interface headers for development mapping
set(PIDGIN_HEADERS
    gtkaccount.h
    gtkblist.h
    gtkblist-theme.h
    gtkblist-theme-loader.h
    gtkcertmgr.h
    gtkcellrendererexpander.h
    gtkcmime.h
    gtkconv.h
    gtkconv-theme.h
    gtkconv-theme-loader.h
    gtkdebug.h
    gtkdialogs.h
    gtkdnd-hints.h
    gtkeventloop.h
    gtkft.h
    gtkicon-theme.h
    gtkicon-theme-loader.h
    gtkidle.h
    gtkimhtml.h
    gtkimhtmltoolbar.h
    gtklog.h
    pidgin.h
    gtkmedia.h
    gtkmenutray.h
    gtknotify.h
    gtkplugin.h
    gtkpluginpref.h
    gtkpounce.h
    gtkprefs.h
    gtkprivacy.h
    gtkrequest.h
    gtkroomlist.h
    gtksavedstatuses.h
    gtkscrollbook.h
    gtksound.h
    gtksourceiter.h
    gtksourceundomanager.h
    gtkstatus-lists.h
    gtkstatusbox.h
    gtkthemes.h
    gtkutils.h
    gtkwhiteboard.h
    pidginstock.h
)

# Define the final executable binary target
add_executable(pidgin ${PIDGIN_SOURCES})

# Specify target specific include directories
target_include_directories(pidgin PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_BINARY_DIR}
)

# Link Pidgin executable with libpurple core and external UI libraries
target_link_libraries(pidgin PRIVATE
    purple                  # Our core library from libpurple directory
    ${GTK_LIBRARIES}        # GTK libraries found by root PkgConfig
    ${GLIB_LIBRARIES}       # Glib core dependencies
)

# Compile flags specific to the Pidgin UI executable
target_compile_definitions(pidgin PRIVATE -DPIDGIN_NAME="Pidgin")

# Installation rules for standard user environments
install(TARGETS pidgin DESTINATION bin)
install(FILES ${PIDGIN_HEADERS} DESTINATION include/pidgin)
