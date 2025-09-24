`libuvc` is a cross-platform library for USB video devices, built atop `libusb`.
It enables fine-grained control over USB video devices exporting the standard USB Video Class
(UVC) interface, enabling developers to write drivers for previously unsupported devices,
or just access UVC devices in a generic fashion.

## Getting and Building libuvc

Prerequisites: You will need `libusb` and [CMake](http://www.cmake.org/) installed.

To build, you can just run these shell commands:

    git clone https://github.com/libuvc/libuvc
    cd libuvc
    mkdir build
    cd build
    cmake ..
    make && sudo make install

and you're set! If you want to change the build configuration, you can edit `CMakeCache.txt`
in the build directory, or use a CMake GUI to make the desired changes.

There is also `BUILD_EXAMPLE` and `BUILD_TEST` options to enable the compilation of `example` and `uvc_test` programs. To use them, replace the `cmake ..` command above with `cmake .. -DBUILD_TEST=ON -DBUILD_EXAMPLE=ON`.
Then you can start them with `./example` and `./uvc_test` respectively. Note that you need OpenCV to build the later (for displaying image).

### Building with 16 KB page size (Android compatibility)

Some Android storefronts now require native libraries to be linked with 16 KB ELF page
sizes. When cross-compiling libuvc with the Android NDK you can enable this alignment
directly from CMake:

```
cmake .. -DLIBUVC_PAGE_SIZE=16384
```

This injects `-Wl,-z,max-page-size=16384 -Wl,-z,common-page-size=16384` into the
generated link commands for the libuvc shared objects. Combine the option with your
existing Android toolchain configuration flags (such as `-DANDROID_ABI` and
`-DANDROID_PLATFORM`) to produce `.so` files that satisfy the Play Store requirement.

## Developing with libuvc

The documentation for `libuvc` can currently be found at https://libuvc.github.io/.

Happy hacking!
