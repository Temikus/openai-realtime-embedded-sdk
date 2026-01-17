set(PEER_PROJECT_PATH "../../deps/libpeer")

# Include all source files - sctp.c has internal CONFIG_USE_USRSCTP guards
file(GLOB CODES "${PEER_PROJECT_PATH}/src/*.c")

idf_component_register(
  SRCS ${CODES}
  INCLUDE_DIRS "${PEER_PROJECT_PATH}/src"
  REQUIRES mbedtls srtp json esp_netif
)

if(NOT IDF_TARGET STREQUAL linux)
  add_definitions("-DESP32")
  # Use LWIP for network operations instead of Linux ifaddrs
  target_compile_definitions(${COMPONENT_LIB} PRIVATE CONFIG_USE_LWIP=1)
  # Set byte order for correct RTP header handling (required by libpeer 9135cde)
  target_compile_definitions(${COMPONENT_LIB} PRIVATE __BYTE_ORDER=__LITTLE_ENDIAN)
  # Set buffer sizes as per libpeer defaults
  target_compile_definitions(${COMPONENT_LIB} PRIVATE CONFIG_AUDIO_BUFFER_SIZE=8096)
  target_compile_definitions(${COMPONENT_LIB} PRIVATE CONFIG_DATA_BUFFER_SIZE=102400)
endif()

# Disable USRSCTP (not available on ESP32)
target_compile_definitions(${COMPONENT_LIB} PRIVATE CONFIG_USE_USRSCTP=0)

add_definitions("-DHTTP_DO_NOT_USE_CUSTOM_CONFIG -DMQTT_DO_NOT_USE_CUSTOM_CONFIG -DDISABLE_PEER_SIGNALING=true")

# Suppress warnings treated as errors in libpeer
target_compile_options(${COMPONENT_LIB} PRIVATE -Wno-restrict -Wno-unused-function)
