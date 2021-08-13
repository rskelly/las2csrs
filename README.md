# las2csrs

This is a tool for converting LiDAR point clouds (in LAS format) to NAD83(CSRS) and between epochs.

Note: project has been dormant for some time. Paths may need to be juggled or code edited to get it working. It builds, at least.

## Dependencies

[libLAS](https://github.com/liblas/libLAS)
Boost
Proj4
GDAL

## Files

src/ - The single source file. 
share/ - A Helmert transformation parameter db and the NAD83v6VG grid shift file in TIF format.
CMakeLists.txt - The build file.
README.md - This file

## Building

This is best done on a Debian/Ubuntu or similar machine:

1) Install the libraries.

    sudo apt install-dev libgdal-dev libproj-dev

2) Install libLAS (no longer in the apt repo; must install from source).

3) Clone and build las2csrs

    git clone https://github.com/rskelly/las2csrs
    cd las2csrs && mkdir build && cd build
    cmake ..
    make

4) Run

    bin/las2csrs

