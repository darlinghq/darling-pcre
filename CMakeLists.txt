project(libpcre)

cmake_minimum_required(VERSION 2.4.0)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)


set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc -D__DARWIN_UNIX03 -fPIC -w")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -nostdinc -nostdinc++ -D__DARWIN_UNIX03 -fPIC -w")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -nostdlib -Wl,--unresolved-symbols=ignore-all -Wl,--version-script=${DARLING_TOP_DIRECTORY}/darwin.map")
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/pcre)

add_definitions(-DHAVE_CONFIG_H)

set(pcre_SRCS
   pcre/pcre_chartables.c
   pcre/pcre_compile.c
   pcre/pcre_config.c
   pcre/pcre_dfa_exec.c
   pcre/pcre_exec.c
   pcre/pcre_fullinfo.c
   pcre/pcre_get.c
   pcre/pcre_globals.c
   pcre/pcre_info.c
   pcre/pcre_maketables.c
   pcre/pcre_newline.c
   pcre/pcre_ord2utf8.c
   pcre/pcre_refcount.c
   pcre/pcre_study.c
   pcre/pcre_tables.c
   pcre/pcre_try_flipped.c
   pcre/pcre_ucd.c
   pcre/pcre_valid_utf8.c
   pcre/pcre_version.c
   pcre/pcre_xclass.c

)

SET(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}/darling")
SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE) 
SET(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

add_library(pcre SHARED ${pcre_SRCS})
target_link_libraries(pcre system)

install(TARGETS pcre DESTINATION ${CMAKE_INSTALL_LIBDIR}/darling)
