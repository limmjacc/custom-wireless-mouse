# SPDX-License-Identifier: Apache-2.0
#
# Picked up by the Zephyr build system as this repository's module CMake
# entry point (see zephyr/module.yml). Not the application build — that's
# app/CMakeLists.txt, built via `west build -b cwm_nrf52810 app`.

zephyr_include_directories(include)

add_subdirectory(drivers)
