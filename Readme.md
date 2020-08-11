## Purley Platforms

The fork from [edk2-platforms](https://github.com/tianocore/edk2-platforms/blob/about/Readme.md)
master branch with Intel Purley Server platforms support [(License)](Info/License.txt).

## How to build (Linux Environment)

## Obtaining source code
1. Create a new folder (directory) on your local development machine
   for use as your workspace. This example uses `/work/git/tianocore`, modify as
   appropriate for your needs.
   ```
   $ export WORKSPACE=/work/git/tianocore
   $ mkdir -p $WORKSPACE
   $ cd $WORKSPACE
   ```

1. Into that folder, clone:
   - [edk2](https://github.com/tianocore/edk2)
   - [purley-platforms](https://github.com/maxpoliak/purley-platforms.git)
   - [edk2-non-osi](https://github.com/tianocore/edk2-non-osi) (if building
      platforms that need it)
   ```
   $ git clone https://github.com/tianocore/edk2.git
   $ git submodule update --init
   ...
   $ git clone https://github.com/maxpoliak/purley-platforms.git
   ...
   $ git clone https://github.com/tianocore/edk2-non-osi.git
   ```

1. Set up a **PACKAGES_PATH** to point to the locations of these three
   repositories:

   `$ export PACKAGES_PATH=$PWD/edk2:$PWD/purley-platforms:$PWD/edk2-non-osi`

## Manual building

1. Set up the build environment (this will modify your environment variables)

   `$ . edk2/edksetup.sh`

   (This step _depends_ on **WORKSPACE** being set as per above.)
1. Build BaseTools

   `make -C edk2/BaseTools`

   (BaseTools can currently not be built in parallel, so do not specify any `-j`
   option, either on the command line or in a **MAKEFLAGS** environment
   variable.)

### Build options
There are a number of options that can (or must) be specified at the point of
building. Their default values are set in `edk2/Conf/target.txt`. If we are
working only on a single platform, it makes sense to just update this file.

target.txt option | command line | Description
------------------|--------------|------------
ACTIVE_PLATFORM   | `-p`         | Description file (.dsc) of platform.
TARGET            | `-b`         | One of DEBUG, RELEASE or NOOPT.
TARGET_ARCH       | `-a`         | Architecture to build for.
TOOL_CHAIN_TAG    | `-t`         | Toolchain profile to use for building.

There is also MAX_CONCURRENT_THREAD_NUMBER (`-n`), roughly equivalent to
`make -j`.

When specified on command line, `-b` can be repeated multiple times in order to
build multiple targets sequentially.

After a successful build, the resulting images can be found in
`Build/{Platform Name}/{TARGET}_{TOOL_CHAIN_TAG}/FV`.

### Build a platform

# Supported Platforms

* [Olympus](Platform/Intel/PurleyOpenBoardPkg/BoardMtOlympus)

For more information, see the
[EDK II Minimum Platform Specification](https://edk2-docs.gitbooks.io/edk-ii-minimum-platform-specification).
