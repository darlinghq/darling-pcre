project(libpcre)

cmake_minimum_required(VERSION 3.10)

if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)


set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdinc -D__DARWIN_UNIX03 -fPIC -w")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -nostdinc -nostdinc++ -D__DARWIN_UNIX03 -fPIC -w")
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/pcre)

add_definitions(-DHAVE_CONFIG_H)

set(pcre_SRCS
   pcre/pcre_byte_order.c
   pcre/pcre_chartables.c
   pcre/pcre_compile.c
   pcre/pcre_config.c
   pcre/pcre_dfa_exec.c
   pcre/pcre_exec.c
   pcre/pcre_fullinfo.c
   pcre/pcre_get.c
   pcre/pcre_globals.c
   pcre/pcre_jit_compile.c
   pcre/pcre_maketables.c
   pcre/pcre_newline.c
   pcre/pcre_ord2utf8.c
   pcre/pcre_refcount.c
   pcre/pcre_string_utils.c
   pcre/pcre_study.c
   pcre/pcre_tables.c
   pcre/pcre_ucd.c
   pcre/pcre_valid_utf8.c
   pcre/pcre_version.c
   pcre/pcre_xclass.c

)

set(DYLIB_INSTALL_NAME "/usr/lib/libpcre.0.dylib")
add_darling_library(pcre SHARED ${pcre_SRCS})
make_fat(pcre)
set_target_properties(pcre PROPERTIES OUTPUT_NAME "pcre.0")
target_link_libraries(pcre system)

InstallSymlink("libpcre.0.dylib" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/lib/libpcre.dylib")
install(TARGETS pcre DESTINATION libexec/darling/usr/lib)

add_darling_executable(pcregrep pcre/pcregrep.c)
target_link_libraries(pcregrep system pcre)

add_darling_executable(pcretest pcre/pcretest.c pcre/pcre_printint.c)
target_link_libraries(pcretest system pcre)

set(DYLIB_INSTALL_NAME "/usr/lib/libpcreposix.0.dylib")
add_darling_library(pcreposix SHARED pcre/pcreposix.c)
make_fat(pcreposix)
set_target_properties(pcreposix PROPERTIES OUTPUT_NAME "pcreposix.0")
target_link_libraries(pcreposix system pcre)

InstallSymlink("libpcreposix.0.dylib" "${CMAKE_INSTALL_PREFIX}/libexec/darling/usr/lib/libpcreposix.dylib")
install(TARGETS pcreposix DESTINATION libexec/darling/usr/lib)

install(TARGETS pcregrep pcretest DESTINATION libexec/darling/usr/bin)

install(FILES
	pcre/doc/pcre-config.1
	pcre/doc/pcregrep.1
	pcre/doc/pcretest.1

	DESTINATION libexec/darling/usr/share/man/man1
)

install(FILES
	pcre/doc/pcre.3
	pcre/doc/pcre_assign_jit_stack.3
	pcre/doc/pcre_compile.3
	pcre/doc/pcre_compile2.3
	pcre/doc/pcre_config.3
	pcre/doc/pcre_copy_named_substring.3
	pcre/doc/pcre_copy_substring.3
	pcre/doc/pcre_dfa_exec.3
	pcre/doc/pcre_exec.3
	pcre/doc/pcre_free_study.3
	pcre/doc/pcre_free_substring.3
	pcre/doc/pcre_free_substring_list.3
	pcre/doc/pcre_fullinfo.3
	pcre/doc/pcre_get_named_substring.3
	pcre/doc/pcre_get_stringnumber.3
	pcre/doc/pcre_get_stringtable_entries.3
	pcre/doc/pcre_get_substring.3
	pcre/doc/pcre_get_substring_list.3
	pcre/doc/pcre_jit_exec.3
	pcre/doc/pcre_jit_stack_alloc.3
	pcre/doc/pcre_jit_stack_free.3
	pcre/doc/pcre_maketables.3
	pcre/doc/pcre_pattern_to_host_byte_order.3
	pcre/doc/pcre_refcount.3
	pcre/doc/pcre_study.3
	pcre/doc/pcre_utf16_to_host_byte_order.3
	pcre/doc/pcre_utf32_to_host_byte_order.3
	pcre/doc/pcre_version.3
	pcre/doc/pcre16.3
	pcre/doc/pcre32.3
	pcre/doc/pcreapi.3
	pcre/doc/pcrebuild.3
	pcre/doc/pcrecallout.3
	pcre/doc/pcrecompat.3
	pcre/doc/pcrecpp.3
	pcre/doc/pcredemo.3
	pcre/doc/pcrejit.3
	pcre/doc/pcrelimits.3
	pcre/doc/pcrematching.3
	pcre/doc/pcrepartial.3
	pcre/doc/pcrepattern.3
	pcre/doc/pcreperform.3
	pcre/doc/pcreposix.3
	pcre/doc/pcreprecompile.3
	pcre/doc/pcresample.3
	pcre/doc/pcrestack.3
	pcre/doc/pcresyntax.3
	pcre/doc/pcreunicode.3

	DESTINATION libexec/darling/usr/share/man/man3
)
