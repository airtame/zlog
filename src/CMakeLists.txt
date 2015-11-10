aux_source_directory(. SRCS)
if (NOT WIN32)
    list(REMOVE_ITEM SRCS ./zlog_win.c)
endif ()

list (REMOVE_ITEM SRCS ./zlog-chk-conf.c)

add_library (zlog
    SHARED
    ${SRCS}
    )

target_link_libraries (zlog pthread)

if (WIN32)
    target_link_libraries (zlog
        unixem
        Ws2_32
        )
endif()

set_target_properties(zlog PROPERTIES PREFIX "")

install(TARGETS zlog
    COMPONENT zlog
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
    )

install(FILES
    zlog.h
    COMPONENT zlog
    DESTINATION include
    )
