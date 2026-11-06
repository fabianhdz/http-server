# HTTP Server

A C17 project for developing an HTTP server from TCP primitives.

Currently, the executable starts and exits successfully. Networking and HTTP
behavior are planned and have not been implemented.

## Build and run

Requirements: a C17 compiler, CMake 3.16 or newer, and a native build tool such as
GNU Make. Development currently targets Linux, including WSL2.

From this directory:

```sh
cmake -S . -B build
cmake --build build
./build/http-server
```

## Development checks

GCC and Clang builds enable compiler warnings. For an address and
undefined-behavior sanitizer build:

```sh
cmake -S . -B build-sanitize -DENABLE_SANITIZERS=ON
cmake --build build-sanitize
./build-sanitize/http-server
```

There are no application tests yet because no server behavior exists. Add native
tests alongside the behavior they exercise. The build and executable require no
parent directory files or external test services.
