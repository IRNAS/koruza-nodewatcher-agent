cmake_minimum_required(VERSION 2.6)

project(koruza-nodewatcher-agent C)
add_definitions(-Os -Wall -Werror --std=gnu99 -Wmissing-declarations)

set(CMAKE_SHARED_LIBRARY_LINK_C_FLAGS "")

include(FindPkgConfig)

pkg_search_module(JSONC json-c)
if(JSONC_FOUND)
  include_directories(${JSONC_INCLUDE_DIRS})
endif()

find_path(ubus_include_dir libubus.h)
include_directories(${ubus_include_dir})

find_path(ubox_include_dir libubox/blobmsg_json.h)
include_directories(${ubox_include_dir})

find_path(uci_include_dir uci.h)
include_directories(${uci_include_dir})

find_path(agent_include_dir nodewatcher-agent/module.h)
include_directories(${agent_include_dir})

find_library(agent_library NAMES nodewatcher-agent-common)

add_library(koruza_module MODULE main.c)
target_link_libraries(koruza_module ${agent_library})
set_target_properties(koruza_module PROPERTIES OUTPUT_NAME koruza PREFIX "")

install(TARGETS koruza_module LIBRARY DESTINATION lib/nodewatcher-agent)
