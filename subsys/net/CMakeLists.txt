# SPDX-License-Identifier: Apache-2.0

zephyr_library()
zephyr_library_property(ALLOW_EMPTY TRUE)
zephyr_library_sources_ifdef(CONFIG_NET_HOSTNAME_ENABLE hostname.c)

if(CONFIG_NETWORKING)
  add_subdirectory(l2)
  add_subdirectory(pkt_filter)

  if(CONFIG_NET_RAW_MODE)
    zephyr_library_sources(ip/net_pkt.c)
  else()
    add_subdirectory(ip)
  endif()
endif()

add_subdirectory(lib)

if(CONFIG_NET_CONNECTION_MANAGER)
  add_subdirectory(conn_mgr)
endif()
