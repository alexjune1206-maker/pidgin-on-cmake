# ==============================================================================
# PIDGIN / LIBPURPLE - CMake Build System Migration
# ==============================================================================
cmake_minimum_required(VERSION 3.16)
project(pidgin 
        VERSION 2.14.14 
        LANGUAGES C CXX)

# Version Definitions (Mapped from m4_define macros)
set(PURPLE_MAJOR_VERSION 2)
set(PURPLE_MINOR_VERSION 14)
set(PURPLE_MICRO_VERSION 14)
set(PURPLE_VERSION "${PURPLE_MAJOR_VERSION}.${PURPLE_MINOR_VERSION}.${PURPLE_MICRO_VERSION}")
set(DISPLAY_VERSION "${PURPLE_VERSION}")

# 1. Global Build Options (Replaces AC_ARG_ENABLE / AC_ARG_WITH)
option(ENABLE_GTKUI "Compile with GTK+ user interface" ON)
option(ENABLE_CONSOLEUI "Compile with console user interface (Finch)" ON)
option(ENABLE_I18N "Install translation files" ON)
option(ENABLE_DBUS "Enable D-Bus support" ON)
option(ENABLE_GSTREAMER "Enable GStreamer audio support" ON)
option(ENABLE_VV "Enable Voice and Video support" ON)
option(ENABLE_PERL "Enable Perl scripting support" ON)
option(ENABLE_TCL "Enable Tcl scripting support" ON)
option(ENABLE_DEBUG "Compile with debugging support" OFF)
option(ENABLE_PLUGINS "Compile with plugin support" ON)

if(ENABLE_DEBUG)
    add_compile_definitions(DEBUG=1)
endif()

# 2. System Structure & Header Checks (Replaces AC_CHECK_HEADERS)
include(CheckIncludeFile)
include(CheckFunctionExists)
include(CheckStructHasMember)

check_include_file("arpa/nameser_compat.h" HAVE_ARPA_NAMESER_COMPAT_H)
check_include_file("fcntl.h" HAVE_FCNTL_H)
check_include_file("sys/time.h" HAVE_SYS_TIME_H)
check_include_file("unistd.h" HAVE_UNISTD_H)
check_include_file("locale.h" HAVE_LOCALE_H)
check_include_file("signal.h" HAVE_SIGNAL_H)
check_include_file("stdint.h" HAVE_STDINT_H)
check_include_file("regex.h" HAVE_REGEX_H)
check_include_file("sys/param.h" HAVE_PARAM_H)
check_include_file("sys/socket.h" HAVE_SYS_SOCKET_H)

check_struct_has_member("struct sockaddr" sa_len "sys/socket.h" HAVE_STRUCT_SOCKADDR_SA_LEN)

# Standard library function checks
check_function_exists(strdup HAVE_STRDUP)
check_function_exists(strstr HAVE_STRSTR)
check_function_exists(atexit HAVE_ATEXIT)
check_function_exists(setlocale HAVE_SETLOCALE)
check_function_exists(inet_ntop HAVE_INET_NTOP)
check_function_exists(getifaddrs HAVE_GETIFADDRS)

# 3. Detect External System Dependencies (Replaces PKG_CHECK_MODULES)
include(FindPkgConfig)
pkg_check_modules(GLIB REQUIRED glib-2.0>=2.16.0  gobject-2.0 gmodule-2.0 gthread-2.0)
pkg_check_modules(LIBXML REQUIRED libxml-2.0>=2.6.0)

# Conditional check for GTK+ UI dependencies
if(ENABLE_GTKUI)
    pkg_check_modules(GTK REQUIRED gtk+-2.0>=2.10.0)
    pkg_check_modules(PANGO pango>=1.4.0)
    if(PANGO_FOUND)
        add_compile_definitions(HAVE_PANGO14=1)
    endif()
endif()

# Conditional check for Console UI dependencies (GNT/ncurses)
if(ENABLE_CONSOLEUI)
    pkg_check_modules(LIBGNT REQUIRED gnt>=2.14.0)
    pkg_check_modules(NCURSESW ncursesw panelw)
    if(NOT NCURSESW_FOUND)
        # Fallback to standard ncurses if wide variant is missing
        pkg_check_modules(NCURSES REQUIRED ncurses panel)
        add_compile_definitions(NO_WIDECHAR=1)
    endif()
endif()

# GStreamer & Farstream check for Audio/Video multimedia structures
if(ENABLE_GSTREAMER)
    pkg_check_modules(GSTREAMER gstreamer-1.0)
    if(GSTREAMER_FOUND)
        add_compile_definitions(USE_GSTREAMER=1)
        if(ENABLE_VV)
            pkg_check_modules(GSTVIDEO gstreamer-video-1.0)
            pkg_check_modules(FARSTREAM farstream-0.2>=0.2.7)
            if(GSTVIDEO_FOUND AND FARSTREAM_FOUND)
                add_compile_definitions(USE_VV=1)
            endif()
        endif()
    endif()
endif()

# D-Bus IPC support verification
if(ENABLE_DBUS)
    pkg_check_modules(DBUS dbus-1>=0.60 dbus-glib-1>=0.60)
    if(DBUS_FOUND)
        add_compile_definitions(HAVE_DBUS=1)
        find_program(PYTHON3_BIN python3) # Required for generating D-Bus bindings source files
    endif()
endif()

# 4. Generate C Preprocessor Config Header (Replaces AC_CONFIG_HEADERS)
configure_file(config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h)
add_compile_definitions(HAVE_CONFIG_H=1)

# 5. Dynamic generation target for package_revision.h (Mapped from Makefile.am target)
add_custom_target(package_revision_check ALL
    COMMAND ${CMAKE_COMMAND} -E echo "#define REVISION \"cmake-build\"" > ${CMAKE_CURRENT_BINARY_DIR}/package_revision.h
    COMMENT "Generating package_revision.h header file"
)

# 6. Source Tree Subdirectories Mapping (Mapped from SUBDIRS)
# Note: Subdirectories must contain their own inner CMakeLists.txt files
add_subdirectory(libpurple)
add_subdirectory(doc)

if(ENABLE_CONSOLEUI)
    add_subdirectory(finch)
endif()

if(ENABLE_GTKUI)
    add_subdirectory(pidgin)
endif()

add_subdirectory(share/sounds)
