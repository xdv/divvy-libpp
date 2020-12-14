# divvy-libpp

[![Build Status](https://travis-ci.org/xdv/divvy-libpp.svg?branch=master)](https://travis-ci.org/xdv/divvy-libpp)
[![Build status](https://ci.appveyor.com/api/projects/status/wk1sgwfi5e35y4lt?svg=true)](https://ci.appveyor.com/project/xdv/divvy-libpp)
[![codecov](https://codecov.io/gh/xdv/divvy-libpp/branch/master/graph/badge.svg)](https://codecov.io/gh/xdv/divvy-libpp)

Divvyd-compatible serialization and transaction signing sample/demo

## Introduction

Demo application that uses the 
([divvyd](https://github.com/divvy/divvyd)).
C++ library to create, sign, and serialize
[Divvy](https://xdv.io) transactions before
submission to the Divvy Consensus Ledger
([divvyd](https://github.com/xdv/divvyd)).
This demonstrates much of the functionality of the
[`sign`](https://xdv.io/build/divvyd-apis/#sign)
RPC function without the overhead of a JSON library,
network delays, needing to trust a 3rd party's divvyd,
nor needing to run your own divvyd.

## Table of contents

* [Dependencies](#dependencies)
  * [Divvyd submodule](#divvyd-submodule)
  * [Other dependencies](#other-dependencies)
* [Demo](#demo)
  * [Additional dependencies](#additional-dependencies)
  * [Build and run](#build-and-run)

## Dependencies

### Divvyd submodule

divvy-libpp includes a git submodule to include the divvyd
source code, which is not cloned by default. To get the
divvyd source, either clone this repository using
```
$ git clone --recursive <location>
```
or after cloning, run the following commands
```
$ git submodule init
$ git submodule update
```

Note: even though the entire divvyd source tree is included
in the submodule, only a subset of it is used by the library.

### Other dependencies

* C++14 or greater
* [Boost](http://www.boost.org/)
* [OpenSSL](https://www.openssl.org/)

## Demo

Code examples are provided in `src/test/divvy-libpp_demo.cpp`
to demonstrate how to create, sign, and verify the signature of a
transaction. Building and running this demo is an optional step to
verify that dependencies are installed and available as expected.

Note that the demo is not a comprehensive suite of tests of the
relevant divvyd functionality; that is covered by divvyd's unit
tests.

### Additional dependencies

In addition to the Usage [dependencies](#dependencies), building
the demo requires

* [cmake](https://cmake.org)

### Build and run

For linux and other unix-like OSes, run the following commands:

```
$ cd ${YOUR_DIVVY_LIBPP_DIRECTORY}
$ mkdir -p build/debug
$ cd build/debug
$ cmake ../.. -DCMAKE_BUILD_TYPE=Debug
$ cmake --build .
$ ./divvylibppdemo
```

For 64-bit Windows, open a MSBuild Command Prompt for Visual Studio
and run the following commands:

```
> cd %YOUR_DIVVY_LIBPP_DIRECTORY%
> mkdir build
> cd build
> cmake -G"Visual Studio 15 2017 Win64" ..
> cmake --build .
> .\Debug\divvylibppdemo.exe
```

32-bit Windows builds are not supported.
