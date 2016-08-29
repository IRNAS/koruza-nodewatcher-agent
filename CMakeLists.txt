cmake_minimum_required(VERSION 2.6)

project(koruza-nodewatcher-agent C)
add_definitions(-Os -Wall -Werror --std=gnu99 -Wmissing-declarations)

set(CMAKE_SHARED_LIBRARY_LINK_C_FLAGS "")

set(SOURCES
  main.c
)

set(LIBS
  nodewatcher-agent-common
)

add_library(koruza_module MODULE main.c)
target_link_libraries(koruza_module ${LIBS})
set_target_properties(koruza_module PROPERTIES OUTPUT_NAME koruza PREFIX "")

install(TARGETS koruza_module LIBRARY DESTINATION lib/nodewatcher-agent)
