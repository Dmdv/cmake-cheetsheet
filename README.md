# cmake-cheetsheet

## How to build

```bash
mkdir -p build
cd build
cmake ..
cmake --build .
```

## Discovering the operating system

```cmake
if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
  message(STATUS "Configuring on/for Linux")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
  message(STATUS "Configuring on/for macOS")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Windows")
  message(STATUS "Configuring on/for Windows")
elseif(CMAKE_SYSTEM_NAME STREQUAL "AIX")
  message(STATUS "Configuring on/for IBM AIX")
else()
  message(STATUS "Configuring on/for ${CMAKE_SYSTEM_NAME}")
endif()
```

## Detecting the Boost libraries

In case we want filesystem component

```cmake
find_package(Boost 1.54 REQUIRED COMPONENTS filesystem)
```

## Detecting external libraries

```cmake
find_package(PkgConfig REQUIRED QUIET)
```

When pkg-config is found, we will have access to the pkg_search_module function to search  
for any library or program that ships a package configuration .pc file.  
In our case, we look for the ZeroMQ library:  

```cmake
pkg_search_module(
  ZeroMQ
  REQUIRED
    libzeromq libzmq lib0mq
  IMPORTED_TARGET
  )
```

Print status message if the ZeroMQ library was found:

```cmake
if(TARGET PkgConfig::ZeroMQ)
  message(STATUS "Found ZeroMQ")
endif()
```
