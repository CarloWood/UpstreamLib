# UpstreamLib

An example project that builds a static library (`libFruitsLib.a`).

It also creates a [cmake package](https://cmake.org/cmake/help/latest/manual/cmake-packages.7.html)
with a config file (`FruitsConfig.cmake`).

To simply build and install the library, run

    $ cmake -S . -B build -DCMAKE_INSTALL_PREFIX:PATH=/tmp/UpstreamLib
    $ gmake -C build install

and find the result as `build/libFruitsLib.a` and installed in `/tmp/UpstreamLib/lib/libFruitsLib.a`.

After installation, another cmake project can use it by
adding&mdash; for example&mdash; the following to its `CMakeLists.txt`:

    find_package(Fruits CONFIG)

which provides the target `Upstream::FruitsLib`.

Note: in the case of a non-standard install path you have to tell that
project where to look for `Fruits`, of course. E.g.:

    $ cmake -S . -B build -DCMAKE_PREFIX_PATH=/tmp/UpstreamLib
