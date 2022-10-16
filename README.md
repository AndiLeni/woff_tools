# woff tools

## Description

This package bundles google/woff2 for .ttf to .woff2 conversion and wget/sfnt2woff for .ttf to .woff conversion.

Builds for Windows are provided as releases and can be found in the `/bin` directory.

## Required changes to submodules

-   google/woff2: no changes
-   wget/sfnt2woff:

    -   `woff2sfnt.c`:
        add to fix O_BINARY build error (see: https://github.com/bramstein/sfnt2woff-zopfli/issues/7), insert after last #include.

        ```c
        #ifdef WIN32
            #include <fcntl.h>
            #include <io.h>

            #if defined(_O_BINARY) && !defined(O_BINARY)
                #define O_BINARY _O_BINARY
                #define setmode  _setmode
                #define fileno   _fileno
            #endif
        #endif
        ```

## Build instructions

Requirements: MSYS2 (https://www.msys2.org/)

1. Start the MINGW64 MSYS2 shell
2. install the build tools
    - `pacman -S mingw-w64-x86_64-toolchain` for 64bit
3. navigate to the sfnt2woff or woff2 directory
4. run `make all` to build
5. woff2 is written in c++ so copy `libstdc++-6.dll` from `C:\msys64\mingw64\bin` to the same directory where the .exe files are

## License

All rights go to the original authors.
