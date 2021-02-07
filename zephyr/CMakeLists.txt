if(CONFIG_MSGPACK)

IF (CONFIG_MSGPACK_BIGENDIAN)
    SET(MSGPACK_ENDIAN_BIG_BYTE 1)
    SET(MSGPACK_ENDIAN_LITTLE_BYTE 0)
ELSE ()
    SET(MSGPACK_ENDIAN_BIG_BYTE 0)
	SET(MSGPACK_ENDIAN_LITTLE_BYTE 1)
ENDIF ()

CONFIGURE_FILE (
    ${CMAKE_CURRENT_SOURCE_DIR}/../cmake/sysdep.h.in
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/msgpack/sysdep.h
    @ONLY
)

CONFIGURE_FILE (
    ${CMAKE_CURRENT_SOURCE_DIR}/../cmake/pack_template.h.in
    ${CMAKE_CURRENT_SOURCE_DIR}/../include/msgpack/pack_template.h
    @ONLY
)

zephyr_include_directories (
        ${CMAKE_CURRENT_SOURCE_DIR}/../include
        ${CMAKE_CURRENT_BINARY_DIR}/../include
        ${CMAKE_CURRENT_BINARY_DIR}/../include/msgpack
)
zephyr_library()
zephyr_library_sources(
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/objectc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/unpack.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/version.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/vrefbuffer.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../src/zone.c
)

endif()
