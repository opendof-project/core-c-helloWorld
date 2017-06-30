Description
===========

This is an example of an OpenDOF requestor and provider that implement the Hello World interface. Both the requestor and provider are written as client applications that are designed to connect to an OpenDOF router.

----------

Running the Hello World Provider and Requestor
===========

The configuration for the hello world provider and requestor can be found at the top of the .c file fore each application. The IP address must be set to point to the OpenDOF router. The credentials must also be set to use a a domain, identity, and key that the OpenDOF router supports.

After building the applications, run the both the helloWorldProvider and helloWorldRequestor applications. Either application can be started first, however the requestor only waits for the provider for the configured timeout (default 60 seconds).


----------

Build Instructions
===========

To use [CMake](http://www.cmake.org/) to build the project, create a directory where the hello world provider and requestor will be built, and from that directory run the following commands. (This should be a different build directory from those used to build the OpenDOF libraries.)

- `cmake <path to component>`
- `cmake --build .

In some cases it may be necessary to specify the install location. The first command can be replaced with the following to change the default install location:

- `cmake <path to component> -DCMAKE_INSTALL_PREFIX=<path to alternate install location>`

To cross compile, use a cmake toolchain file for the target platform.

- `cmake <path to component> -DCMAKE_TOOLCHAIN_FILE=<location of platform's toolchain file>`

----------

Build Prerequisites
===========

-   dof-pcr-dev
-   dof-pcr-posix
-   dof-cipher-plugins-dev
-   dof-aes-cipher-plugin
-   dof-oal
-   dof-inet-posix
-   dof-connection-reconnecting-listener
