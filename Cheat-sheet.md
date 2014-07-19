This page lists the commands to invoke to achieve some common build tasks with Meson. Unless otherwise specified all the examples below assume that the build directory is created in a directory called <tt>build</tt> which is located in the source tree's root. It is also assumed that all commands are executed in that directory.

## Producing a coverage report ##

First initialise the build directory with this command.

    meson --enable-gcov ..

Then issue the following commands.

    ninja
    ninja test
    ninja coverage-html (or coverage-xml)

The coverage report can be found in the meson-logs subdirectory.

## Adding some optimization to debug builds ##

By default the debug build does not use any optimizations. This is the desired approach most of the time. However some projects benefit from having some minor optimizations enabled. Gcc even has a specific compiler flag <tt>-Og</tt> for this. To enable its use, just issue the following command.

    mesonconf -Dcargs=-Og

This causes all subsequent builds to use this command line argument.

## Using address sanitizer ##

Clang comes with a selection of analysis tools such as the [address sanitizer](http://clang.llvm.org/docs/AddressSanitizer.html). They are enabled by adding a few compiler flags (requires a relatively recent GCC or Clang).

First we set up meson.

    CFLAGS='-fsanitize=address -fno-omit-frame-pointer' meson ..

This example uses only plain C. For C++ you would set the variable <tt>CXXFLAGS</tt>.

After this you just compile your code and run the test suite. Address sanitizer will abort executables which have bugs so they show up as test failures.

## Using Clang static analyzer ##

The clang compiler comes with a static analysis tool which is invoked by compiling the application via a wrapper command. We will generate this report in a custom build directory and clean it up afterwards so no build artifacts remain lingering anywhere. This is achieved by running the following commands in the root of the source directory.

    mkdir uniquedirname
    cd uniquedirname
    scan-build meson ..
    scan-build ninja
    cd ..
    rm -rf uniquedirname

The static analysis report will be found in the <tt>/tmp</tt> subdirectory, though you can forward it somewhere else if you prefer.