add_executable(wjecli wjecli.c wjecli.h cmds.c)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${ALL_CFLAGS} ${PTHREAD_CFLAGS} ${OPENSSL_CFLAGS}")

target_link_libraries(wjecli
	wjelement
)

install(TARGETS wjecli DESTINATION bin)
install(PROGRAMS wje DESTINATION bin)

# USED FOR LIBFUZZER AND LACK OF MAIN IN WJECLI.c

if (NOT CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
    message(FATAL_ERROR "Clang is required for libFuzzer!")
endif()
target_compile_options(wjecli PUBLIC -fsanitize=fuzzer)
target_link_options(wjecli PUBLIC -fsanitize=fuzzer)