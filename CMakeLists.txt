# Copyright (c) 2017, Panasonic Corporation.
#
# Permission to use, copy, modify, and/or distribute this software for any
# purpose with or without fee is hereby granted, provided that the above
# copyright notice and this permission notice appear in all copies.
#
# THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
# WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
# MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
# ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
# WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
# ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
# OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

cmake_minimum_required( VERSION 2.8 )

project( helloWorldProject )

# Use CMake's find package to verify that the required OpenDOF libraries are available.
# Each OpenDOF component defines a find package that can be searched for. See the Readme for each component for more information.
find_package( dof-pcr-dev 7.0 REQUIRED )
find_package( dof-pcr 2.0 REQUIRED )
find_package( dof-cipher-plugins-dev 1.0 REQUIRED )
find_package( dof-aes-cipher-plugin 1.0 REQUIRED )
find_package( dof-oal 8.0 REQUIRED )
find_package( dof-inet REQUIRED )
find_package( dof-connection-reconnecting-listener 3.0 REQUIRED )

set( CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS} ${CMAKE_C_FLAGS_DEBUG} -g -Wall" )

# Set the directories where include files can be found. If find package command finds the component, it will define a variable that can be used here.
# See the Readme for each OpenDOF component for more information.
include_directories( ${CMAKE_INSTALL_PREFIX}/include ${PCR_DEV_INCLUDE_DIRS} ${PCR_INCLUDE_DIRS} ${DOF_OAL_INCLUDE_DIRS} ${DOF_INET_INCLUDE_DIRS}
                     ${DOF_AES_CIPHER_PLUGIN_INCLUDE_DIRS} ${DOF_CONNECTION_RECONNECTING_LISTENER_INCLUDE_DIRS})

# Specify the executables that will be built and the required source code files for 
add_executable( helloWorldRequestor  ${CMAKE_CURRENT_SOURCE_DIR}/helloWorldRequestor.c )
add_executable( helloWorldProvider  ${CMAKE_CURRENT_SOURCE_DIR}/helloWorldProvider.c )

# Link the executables against the required libraries. If find package command finds the component, it will define a variable that can be used here.
# See the Readme for each OpenDOF component for more information.
if( WIN32 )
    target_link_libraries( helloWorldRequestor ${DOF_CONNECTION_RECONNECTING_LISTENER_LIBRARIES} ${DOF_OAL_LIBRARIES} ${DOF_INET_LIBRARIES} ${DOF_PCR_LIBRARIES} ${DOF_AES_CIPHER_PLUGIN_LIBRARIES}  ${DOF_TWOFISH_CIPHER_PLUGIN_LIBRARIES} ${DOF_SMS4_CIPHER_PLUGIN_LIBRARIES} ws2_32 )
    target_link_libraries( helloWorldprovider ${DOF_CONNECTION_RECONNECTING_LISTENER_LIBRARIES} ${DOF_OAL_LIBRARIES} ${DOF_INET_LIBRARIES} ${DOF_PCR_LIBRARIES} ${DOF_AES_CIPHER_PLUGIN_LIBRARIES}  ${DOF_TWOFISH_CIPHER_PLUGIN_LIBRARIES} ${DOF_SMS4_CIPHER_PLUGIN_LIBRARIES} ws2_32 )
else( WIN32 )
    target_link_libraries( helloWorldRequestor ${DOF_CONNECTION_RECONNECTING_LISTENER_LIBRARIES} ${DOF_OAL_LIBRARIES} ${DOF_INET_LIBRARIES} ${DOF_PCR_LIBRARIES} ${DOF_AES_CIPHER_PLUGIN_LIBRARIES}  ${DOF_TWOFISH_CIPHER_PLUGIN_LIBRARIES} ${DOF_SMS4_CIPHER_PLUGIN_LIBRARIES} pthread )
    target_link_libraries( helloWorldProvider ${DOF_CONNECTION_RECONNECTING_LISTENER_LIBRARIES} ${DOF_OAL_LIBRARIES} ${DOF_INET_LIBRARIES} ${DOF_PCR_LIBRARIES} ${DOF_AES_CIPHER_PLUGIN_LIBRARIES}  ${DOF_TWOFISH_CIPHER_PLUGIN_LIBRARIES} ${DOF_SMS4_CIPHER_PLUGIN_LIBRARIES} pthread )
endif( WIN32 )
