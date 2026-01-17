idf_component_register(
    SRCS "main.cpp" "http.cpp" "media.cpp" "webrtc.cpp" "wifi.cpp"
    INCLUDE_DIRS "."
    REQUIRES peer esp-libopus esp_http_client driver esp_wifi nvs_flash esp_psram
)
