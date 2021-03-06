## Purley Platforms

The fork from [edk2-platforms](https://github.com/tianocore/edk2-platforms/blob/about/Readme.md)
master branch with Intel Purley Server platforms support [(License)](Info/License.txt).

## Manual building (Linux Environment)

1. Create a new folder (directory) on your local development machine
   for use as your workspace
   ```
   $ export WORKSPACE=$(pwd)/tianocore
   $ mkdir -p $WORKSPACE
   $ cd $WORKSPACE
   ```

2. Clone all projects to the $WORKSPACE directory
   ```
   $ git clone https://github.com/maxpoliak/edk2.git -b purley-platforms
   $ cd edk2
   $ git submodule update --init --recursive
   $ cd ..

   $ git clone https://github.com/maxpoliak/edk2-non-osi.git -b purley-platforms

   $ git clone https://github.com/IntelFsp/FSP.git -b KabylakeFsp0001

   $ git clone https://github.com/maxpoliak/purley-platforms.git
   ```

3. Set up a **PACKAGES_PATH** to point to the locations of these three
   repositories:

   `$ export PACKAGES_PATH=$PWD/edk2:$PWD/purley-platforms:$PWD/edk2-non-osi:$PWD/FSP`

4. Set up the build environment (this will modify your environment variables)

   `$ . edk2/edksetup.sh`

   This step _depends_ on **WORKSPACE** being set as per above.

5. Build BaseTools

   `make -C edk2/BaseTools`

   BaseTools can currently not be built in parallel, so do not specify any `-j`
   option, either on the command line or in a **MAKEFLAGS** environment
   variable.

6. Build BaseTools

   ```
   $ cd purley-platforms/Platform/Intel
   $ python build_bios.py --platform BoardMtOlympus --toolchain GCC5
   ```

   After a successful build, the resulting images can be found in
   `Build/{Platform Name}/{TARGET}/{TOOL_CHAIN_TAG}/FV`.

# Supported Platforms

* [Olympus](Platform/Intel/PurleyOpenBoardPkg/BoardMtOlympus)

For more information, see the
[EDK II Minimum Platform Specification](https://edk2-docs.gitbooks.io/edk-ii-minimum-platform-specification).
