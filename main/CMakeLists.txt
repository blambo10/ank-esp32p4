message("Loading nested cmake")
# In your component's CMakeLists.txt
if ("${IDF_TARGET}" STREQUAL "esp32p4" AND "${CONFIG_NAME}" STREQUAL "master_config")
    # target_sources(${COMPONENT_LIB} PRIVATE "master.c")
    # idf_component_register(SRCS "master.c"
    #                        PRIV_REQUIRES driver bt nvs_flash esp_hosted
    #                        INCLUDE_DIRS "")
    set(SRC_FILES "master.c")
elseif ("${IDF_TARGET}" STREQUAL "esp32p4" AND "${CONFIG_NAME}" STREQUAL "slave_config")
    # target_sources(${COMPONENT_LIB} PRIVATE "slave.c")
    # idf_component_register(SRCS "slave.c"
    #                        PRIV_REQUIRES driver bt nvs_flash esp_hosted
    #                        INCLUDE_DIRS "")
    set(SRC_FILES "slave.c")
endif()

# idf_component_register(PRIV_REQUIRES driver bt nvs_flash esp_hosted
#                        INCLUDE_DIRS "")

idf_component_register(SRCS "${SRC_FILES}"
                       PRIV_REQUIRES driver bt nvs_flash esp_hosted
                       INCLUDE_DIRS "")

# idf_component_register(SRCS "main.c"
#                        PRIV_REQUIRES driver bt nvs_flash esp_hosted
#                        INCLUDE_DIRS "")