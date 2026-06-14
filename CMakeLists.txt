cmake_minimum_required(VERSION 3.16)

project(
    cpp_multithreaded_http_server
    VERSION 1.0
    DESCRIPTION "Multithreaded HTTP/1.1 Server in C++"
    LANGUAGES CXX
)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(OpenSSL REQUIRED)

add_executable(server
    httpserver/server.cc

    internal/headers/headers.cc
    internal/requests/request.cc
    internal/response/response.cc
    internal/server_services/http_services.cc
)

target_include_directories(server PRIVATE
    .
    3rd-party-library
)

target_compile_options(server PRIVATE
    -Wall
    -Wextra
    -pthread
)

target_link_libraries(server PRIVATE
    OpenSSL::SSL
    OpenSSL::Crypto
)
