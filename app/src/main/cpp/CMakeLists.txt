cmake_minimum_required(VERSION 3.4.1)

set(distribution_DIR ${CMAKE_SOURCE_DIR}/../../../../ndk/jni)

add_library(libcrypto STATIC IMPORTED)
set_target_properties(libcrypto PROPERTIES IMPORTED_LOCATION
  ${distribution_DIR}/libs/${ANDROID_ABI}/libcrypto.a)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99 -Wall")

add_library(amiitool SHARED
            amiibo.c
            main.c
            drbg.c
            keygen.c
            util.c)

target_include_directories(amiitool PRIVATE
                           ${distribution_DIR}/include)

target_link_libraries(amiitool
                      android
                      libcrypto)
