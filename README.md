GEOS -- Geometry Engine, Open Source
====================================

GEOS is a C++11 library for performing operations on two-dimensional vector
geometries. It is primarily a port of the [JTS Topology
Suite](https://github.com/locationtech/jts) Java library.  It provides many of
the algorithms used by [PostGIS](http://www.postgis.net/), the
[Shapely](https://pypi.org/project/Shapely/) package for Python, the
[sf](https://github.com/r-spatial/sf) package for R, and others.

More information is available the [project homepage](https://trac.osgeo.org/geos).

## Build status

| branch / CI | Debbie | Winnie | Dronie | Travis CI | GitLab CI | AppVeyor | Bessie | Bessie32 |
|:---         |:---    |:---    |:---    |:---       |:---       |:---      |:---    |:---    |
| master      | [![debbie](https://debbie.postgis.net/buildStatus/icon?job=GEOS_Master)](https://debbie.postgis.net/view/GEOS/job/GEOS_Master/) | [![winnie](https://winnie.postgis.net:444/view/GEOS/job/GEOS_Master/badge/icon)](https://winnie.postgis.net:444/view/GEOS/job/GEOS_Master/) | [![dronie](https://drone.osgeo.org/api/badges/geos/geos/status.svg?branch=master)](https://drone.osgeo.org/geos/geos?branch=master) | [![travis](https://travis-ci.com/libgeos/geos.svg?branch=master)](https://travis-ci.com/libgeos/geos?branch=master) | [![gitlab-ci](https://gitlab.com/geos/libgeos/badges/master/build.svg)](https://gitlab.com/geos/libgeos/commits/master) | [![appveyor](https://ci.appveyor.com/api/projects/status/62aplwst722b89au/branch/master?svg=true)](https://ci.appveyor.com/project/dbaston/geos/branch/master) | [![bessie](https://debbie.postgis.net/buildStatus/icon?job=GEOS_Worker_Run/label=bessie&BRANCH=master)](https://debbie.postgis.net/view/GEOS/job/GEOS_Worker_Run/label=bessie) | [![bessie32](https://debbie.postgis.net/buildStatus/icon?job=GEOS_Worker_Run/label=bessie32&BRANCH=master)](https://debbie.postgis.net/view/GEOS/job/GEOS_Worker_Run/label=bessie32) ||
| 3.7     | [![debbie](https://debbie.postgis.net/buildStatus/icon?job=GEOS_Branch_3.7)](https://debbie.postgis.net/view/GEOS/job/GEOS_Branch_3.7/) | [![winnie](https://winnie.postgis.net:444/view/GEOS/job/GEOS_Branch_3.7/badge/icon)](https://winnie.postgis.net:444/view/GEOS/job/GEOS_Branch_3.7/) | [![dronie](https://drone.osgeo.org/api/badges/geos/geos/status.svg?branch=3.7)](https://drone.osgeo.org/geos/geos?branch=3.7) | [![travis](https://travis-ci.com/libgeos/geos.svg?branch=3.7)](https://travis-ci.com/libgeos/geos?branch=3.7) | [![gitlab-ci](https://gitlab.com/geos/libgeos/badges/svn-3.7/build.svg)](https://gitlab.com/geos/libgeos/commits/3.7) | [![appveyor](https://ci.appveyor.com/api/projects/status/62aplwst722b89au/branch/3.7?svg=true)](https://ci.appveyor.com/project/dbaston/geos/branch/3.7) ||
| 3.6     | [![debbie](https://debbie.postgis.net/buildStatus/icon?job=GEOS_Branch_3.6)](https://debbie.postgis.net/view/GEOS/job/GEOS_Branch_3.6/) | [![winnie](https://winnie.postgis.net:444/view/GEOS/job/GEOS_Branch_3.6/badge/icon)](https://winnie.postgis.net:444/view/GEOS/job/GEOS_Branch_3.6/) | [![dronie](https://drone.osgeo.org/api/badges/geos/geos/status.svg?branch=svn-3.6)](https://drone.osgeo.org/geos/geos?branch=svn-3.6) | [![travis](https://travis-ci.com/libgeos/geos.svg?branch=svn-3.6)](https://travis-ci.com/libgeos/geos?branch=svn-3.6) | [![gitlab-ci](https://gitlab.com/geos/libgeos/badges/svn-3.6/build.svg)](https://gitlab.com/geos/libgeos/commits/svn-3.6) | [![appveyor](https://ci.appveyor.com/api/projects/status/62aplwst722b89au/branch/svn-3.6?svg=true)](https://ci.appveyor.com/project/dbaston/geos/branch/svn-3.6) |

## Building GEOS From Source

### Prerequisites

GEOS has no external library dependencies and can be built with any C++11
compiler.

### Unix

GEOS can be built on Unix systems using either the autotools or CMake build
systems.

#### Using Autotools:

When building GEOS using autotools, a `configure` script must first be generated
using the `autogen.sh` file included in the root of the repository:

    ./autogen.sh

An out-of-tree build can then be initiated by creating a subdirectory and
running the generated `configure` script from that subdirectory:

    mkdir obj && cd obj && ../configure

Once the `configure` script has run, GEOS can be built by running `make` and
installed by running `make install`. The test suite can be run using `make
check`.

#### Using CMake:

To build `GEOS` using CMake, create a build directory and run the `cmake` command
from that location:

    mkdir build && cd build && cmake -DCMAKE_BUILD_TYPE=Release ..

Setting `CMAKE_BUILD_TYPE` to `Release` is necessary to enable compiler
optimizations.

Once the `cmake` tool has run, GEOS can be built by running `make` and
installed by running `make install`. The test suite can be run using `make
check`.

### Microsoft Windows

GEOS can be built with Microsoft Visual C++ by opening the `CMakeLists.txt` in
the project root using `File > Open > CMake`.

## Client applications

### Using the C interface

GEOS promises long-term stability of the C API. In general, successive releases
of the C API may add new functions but will not remove or change existing types
or function signatures. The C library uses the C++ interface, but the C library
follows normal ABI-change-sensitive versioning, so programs that link only
against the C library should work without relinking when GEOS is upgraded. For
this reason, it is recommended to use the C API for software that is intended
to be dynamically linked to a system install of GEOS.

The `geos-config` program can be used to determine appropriate compiler and
linker flags for building against the C library:

    CFLAGS += `geos-config --cflags`
    LDFLAGS += `geos-config --ldflags` -lgeos_c

All functionality of the C API is available through the `geos_c.h` header file.

Documentation for the C API is provided via comments in the `geos_c.h` header file.
C API usage examples can be found in the GEOS unit tests and in the source
code of software that uses GEOS, such as PostGIS and the sf package for R.

### Using the C++ interface

The C++ interface to GEOS provides a more natural API for C++ programs, as well
as additional functionality that has not been exposed in the C API.  However,
developers who decide to use the C++ interface should be aware that GEOS does
not promise API or ABI stability of the C++ API between releases.  Breaking
changes in the C++ API/ABI are not typically announced or included in the NEWS
file.

The C++ library name will change on every minor release.

The `geos-config` program can be used to determine appropriate compiler and
linker flags for building against the C++ library:

    CFLAGS += `geos-config --cflags`
    LDFLAGS += `geos-config --ldflags` -lgeos

A compiler warning may be issued when building against the C++ library. To remove
the compiler warning, define `USE_UNSTABLE_GEOS_CPP_API` somewhere in the program.

Commonly-used functionality of GEOS is available in the `geos.h` header file.
Less-common functionality can be accessed by including headers for individual
classes, e.g. `#include <geos/algorithm/distance/DiscreteHausdorffDistance.h>`.

    #include <geos.h>

Documentation for the C++ API is available at https://geos.osgeo.org/doxygen/, and
basic C++ usage examples can be found in `doc/example.cpp`.


### Scripting language bindings

#### Ruby
Ruby bindings are fully supported. To build, use the `--enable-ruby` option
when configuring:

    ./configure .. --enable-ruby

#### PHP

PHP bindings for GEOS are available from the
[php-geos](https://git.osgeo.org/gitea/geos/php-geos) project:

#### Python
Since version 3.0, the Python bindings are unsupported. Recommended options:

 1. Become or recruit a new maintainer.
 2. Use [Shapely](http://pypi.python.org/pypi/Shapely) with Python
    versions 2.4 or greater.
 3. Call functions from `libgeos_c` via Python ctypes.

## Documentation

To build Doxygen documentation:

    cd doc
    make doxygen-html

## Style

To format your code into the desired style, use astyle 3.1
(included in source tree, see tools/astyle)

    astyle --style=stroustrup \
           --unpad-paren \
           --pad-header \
           --pad-comma \
           --indent=spaces=4 \
           --align-pointer=type \
           --max-code-length=120 \
           --lineend=linux \
           yourfile.cpp

