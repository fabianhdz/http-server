cmake_minimum_required(VERSION 3.16)
project(http_server VERSION 0.1.0 LANGUAGES C)

option(ENABLE_SANITIZERS "Enable address and undefined-behavior sanitizers" OFF)

add_executable(http-server src/main.c)
set_target_properties(http-server PROPERTIES
    C_STANDARD 17
    C_STANDARD_REQUIRED YES
    C_EXTENSIONS NO
)

if(CMAKE_C_COMPILER_ID MATCHES "GNU|Clang")
    target_compile_options(http-server PRIVATE
        -Wall -Wextra -Wpedantic -Wconversion -Wshadow
    )
    if(ENABLE_SANITIZERS)
        target_compile_options(http-server PRIVATE
            -fsanitize=address,undefined -fno-omit-frame-pointer -g
        )
        target_link_options(http-server PRIVATE -fsanitize=address,undefined)
    endif()
elseif(ENABLE_SANITIZERS)
    message(FATAL_ERROR "ENABLE_SANITIZERS requires GCC or Clang")
endif()
