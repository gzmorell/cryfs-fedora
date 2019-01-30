
This is RPM sources for building RPM for CryFS

CryFS encrypts your files, so you can safely store them anywhere. It works well together with cloud services like Dropbox, iCloud, OneDrive and others.
See [https://www.cryfs.org](https://www.cryfs.org).

Building from source
====================

Requirements
------------
  - Git (for getting the source code)
  - GCC version >= 4.8 or Clang >= 3.7
  - CMake version >= 2.8
  - libcurl4 (including development headers)
  - Boost libraries version >= 1.56 (including development headers)
    - filesystem
    - system
    - chrono
    - program_options
    - thread
  - Crypto++ version >= 5.6.3 (including development headers)
  - SSL development libraries (including development headers, e.g. libssl-dev)
  - libFUSE version >= 2.8.6 (including development headers), on Mac OS X instead install osxfuse from https://osxfuse.github.io/
  - Python >= 2.7

Install required build tools and dependencies
---------------------------------------------
        # Fedora
        sudo dnf install git gcc-c++ cmake make libcurl-devel boost-devel boost-static cryptopp-devel openssl-devel fuse-devel python

Build & Install
---------------

 1. Clone repository

        $ git clone https://github.com/cryfs/cryfs.git cryfs
        $ cd cryfs

 2. Build

        $ mkdir cmake && cd cmake
        $ cmake ..
        $ make

 3. Install

        $ sudo make install

You can pass the following variables to the *cmake* command (using *-Dvariablename=value*):
 - **-DCMAKE_BUILD_TYPE**=[Release|Debug]: Whether to run code optimization or add debug symbols. Default: Release
 - **-DBUILD_TESTING**=[on|off]: Whether to build the test cases (can take a long time). Default: off
 - **-DCRYFS_UPDATE_CHECKS**=off: Build a CryFS that doesn't check online for updates and security vulnerabilities.

Troubleshooting
---------------

On most systems, CMake should find the libraries automatically. However, that doesn't always work.

1. **Boost headers not found**

    Pass in the boost include path with

        cmake .. -DBoost_INCLUDE_DIRS=/path/to/boost/headers

    If you want to link boost dynamically (e.g. you don't have the static libraries), use the following:

        cmake .. -DBoost_USE_STATIC_LIBS=off

2. **Fuse/Osxfuse library not found**

    Pass in the library path with

        cmake .. -DFUSE_LIB_PATH=/path/to/fuse/or/osxfuse

3. **Fuse/Osxfuse headers not found**

    Pass in the include path with

        cmake .. -DCMAKE_CXX_FLAGS="-I/path/to/fuse/or/osxfuse/headers"

4. **CryptoPP library not found**

    Pass in the library path with

        cmake .. -DCRYPTOPP_LIB_PATH=/path/to/cryptopp

5. **Openssl headers not found**

    Pass in the include path with

        cmake .. -DCMAKE_C_FLAGS="-I/path/to/openssl/include"


Creating .deb and .rpm packages
-------------------------------

There are additional requirements if you want to create packages. They are:
 - CMake version >= 3.3
 - rpmbuild for creating .rpm package

 1. Clone repository

        $ git clone https://github.com/cryfs/cryfs.git cryfs
        $ cd cryfs

 2. Build

        $ mkdir cmake && cd cmake
        $ cmake .. -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=off
        $ make package

