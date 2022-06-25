Cross-compiliation of Pepperscore

Pepperscore can be cross-compiled on Linux to all other supported host systems. This is done by changing the HOST parameter when building the dependencies and then specifying another --prefix directory when building Pepperscore.

The following instructions are only tested on Debian Stretch and Ubuntu Bionic.
MacOSX Cross-compilation

Cross-compiling to MacOSX requires a few additional packages to be installed:

$ sudo apt-get install python3-setuptools libcap-dev zlib1g-dev libbz2-dev

Additionally, the Mac OSX SDK must be downloaded and extracted manually:

$ mkdir -p depends/sdk-sources
$ mkdir -p depends/SDKs
$ curl https://bitcoincore.org/depends-sources/sdks/MacOSX10.11.sdk.tar.gz -o depends/sdk-sources/MacOSX10.11.sdk.tar.gz
$ tar -C depends/SDKs -xf depends/sdk-sources/MacOSX10.11.sdk.tar.gz

When building the dependencies, as described in build-generic, use

$ make HOST=x86_64-apple-darwin11 -j4

When building Pepperscore, use

$ ./configure --prefix=`pwd`/depends/x86_64-apple-darwin11 LDFLAGS="-ldb_cxx"

Windows 64bit/32bit Cross-compilation

Cross-compiling to Windows requires a few additional packages to be installed:

$ sudo apt-get install nsis wine wine64 bc

For Windows 64bit, install :

$ sudo apt-get install g++-mingw-w64-x86-64
$ # Required to enable C++ threading libraries (e.g. std::thread)
$ sudo update-alternatives --set x86_64-w64-mingw32-g++  /usr/bin/x86_64-w64-mingw32-g++-posix
$ sudo update-alternatives --set x86_64-w64-mingw32-gcc  /usr/bin/x86_64-w64-mingw32-gcc-posix

For Windows 32bit, install:

$ sudo apt-get install g++-mingw-w64-i686
$ # Required to enable C++ threading libraries (e.g. std::thread)
$ sudo update-alternatives --set i686-w64-mingw32-gcc /usr/bin/i686-w64-mingw32-gcc-posix
$ sudo update-alternatives --set i686-w64-mingw32-g++  /usr/bin/i686-w64-mingw32-g++-posix

When building the dependencies, as described in build-generic, use

$ make HOST=x86_64-w64-mingw32 -j4

When building Pepperscore, use

$ make distclean

$ ./configure --prefix=`pwd`/depends/x86_64-w64-mingw32 LDFLAGS="-ldb_cxx"

These commands will build for Windows 64bit. If you want to compile for 32bit, replace x86_64-w64-mingw32 with i686-w64-mingw32.


ARM-Linux Cross-compilation

Cross-compiling to ARM-Linux requires a few additional packages to be installed:

$ sudo apt-get install g++-arm-linux-gnueabihf

When building the dependencies, as described in build-generic, use

$ make HOST=arm-linux-gnueabihf -j4

When building Pepperscore, use

$ ./configure --prefix=`pwd`/depends/arm-linux-gnueabihf LDFLAGS="-ldb_cxx"


