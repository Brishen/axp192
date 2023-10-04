if (ESP_PLATFORM)
    idf_component_register(
            SRCS "axp192.c"
            INCLUDE_DIRS "."
            REQUIRES driver esp_timer
    )
    add_definitions("-DAXP192_INCLUDE_SDKCONFIG_H")
endif ()
