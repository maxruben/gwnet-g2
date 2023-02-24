#-------------------------------------------------------------------------------
# Zephyr Example Application
#
# Copyright (c) 2021 Nordic Semiconductor ASA
# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)
find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

project(app LANGUAGES C VERSION 1.0.0)

configure_file(app_version.h.in ${CMAKE_BINARY_DIR}/app/include/app_version.h)

target_sources(app PRIVATE src/main.c)

# Add include directory for board specific CAF def files
zephyr_include_directories(
  configuration/${BOARD}
  )

target_sources_ifdef(CONFIG_CAF_SAMPLE_LED_STATE
  app PRIVATE src/modules/led_state.c)