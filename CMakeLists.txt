cmake_minimum_required (VERSION 2.8)
cmake_policy (SET CMP0015 OLD)

set (CMAKE_BUILD_TYPE "" CACHE STRING "")

project (TMUX)
set (TMUX_VERSION_MAJOR 1)
set (TMUX_VERSION_MINOR 0)

set(Configs tmux.conf)

add_custom_target(config ALL)

foreach(C ${Configs})
    add_custom_command( TARGET config
                        COMMAND ${CMAKE_COMMAND} -E copy
                            ${CMAKE_SOURCE_DIR}/config/${C}
                            ${CMAKE_BINARY_DIR}/config/.${C}
                      )
endforeach()

install( DIRECTORY ${CMAKE_BINARY_DIR}/config/
         DESTINATION ${DESTDIR}/$ENV{HOME}/
       )
