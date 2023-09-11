target_sources(${CMAKE_PROJECT_NAME} PRIVATE
        mpc-flow/mpc-parallel/mpc_context.cpp
        mpc-flow/mpc-parallel/mpc_round.cpp
        mpc-flow/mpc-parallel/LazyBCValidator.cpp
        mpc-flow/mpc-parallel-v2/mpc_context.cpp
        mpc-flow/mpc-parallel-v2/mpc_round.cpp
        )

# Refer to single internal library only if it's not assembled into a big library.
option(ENABLE_ASSEMBLE "Enable assemble" OFF)
if (NOT ${ENABLE_ASSEMBLE})
    #find_package(PkgConfig REQUIRED)
    set(OPENSSL_USE_STATIC_LIBS TRUE)
    #find_package(OpenSSL REQUIRED)
    #设置openssl的库头文件
        set(OPENSSL_INCLUDE_DIR  "${CMAKE_PREFIX_PATH}/include/")
        #设置openssl的库路径
        set(OPENSSL_SSL_LIBRARY "${CMAKE_PREFIX_PATH}/lib/libssl.a")
        #设置openssl的工具库
        set(OPENSSL_CRYPTO_LIBRARY "${CMAKE_PREFIX_PATH}/lib/libcrypto.a")


    target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE
            ${OPENSSL_INCLUDE_DIR}
            )

    target_link_libraries(${CMAKE_PROJECT_NAME} PUBLIC
    OPENSSL_CRYPTO_LIBRARY
            -ldl
            )
endif()
