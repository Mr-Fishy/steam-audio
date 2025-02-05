project(SteamAudio VERSION 4.5.3)

# The following assumes that the platforms are x64
if (APPLE)
    set(SteamAudio_LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/lib/osx")
    set(SteamAudio_LIB_FILE "${SteamAudio_LIB_DIR}/phonon.dylib")
elseif (WIN32)
    set(SteamAudio_LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/lib/windows-x64")
    set(SteamAudio_LIB_FILE "${SteamAudio_LIB_DIR}/phonon.dll")
else ()
    set(SteamAudio_LIB_DIR "${CMAKE_CURRENT_SOURCE_DIR}/lib/linux-x64")
    set(SteamAudio_LIB_FILE "${SteamAudio_LIB_DIR}/libphonon.so")
endif ()

add_library(
    ${PROJECT_NAME} SHARED IMPORTED GLOBAL
)

add_dependencies(
    ${PROJECT_NAME}

    SteamAudioTarget
)

set_target_properties(
    ${PROJECT_NAME} PROPERTIES

    IMPORTED_LOCATION "${SteamAudio_LIB_FILE}"

    INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

if (WIN32)

    set_property(
        TARGET ${PROJECT_NAME}

        PROPERTY IMPORTED_IMPLIB "${SteamAudio_LIB_DIR}/phonon.lib"
    )

endif ()
