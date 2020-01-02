# UpstreamLib

An example project that builds a static library (`libFruitsLib.a`).

It also creates a [cmake package](https://cmake.org/cmake/help/latest/manual/cmake-packages.7.html)
with a config file (`FruitsConfig.cmake`).

To simply build the library, run

    $ cmake -S . -B build
    $ gmake -C build

and find the result as `build/libFruitsLib.a`.

After installation another cmake project can use it by
adding, for example, the following to its `CMakeLists.txt`:

    find_package(Fruits CONFIG)

which provides the target `Upstream::FruitsLib`.
