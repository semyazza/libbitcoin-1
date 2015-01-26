[![Build Status](https://travis-ci.org/libbitcoin/libbitcoin-consensus.svg?branch=master)](https://travis-ci.org/libbitcoin/libbitcoin-consensus)

# Libbitcoin Consensus

*The Bitcoin Consensus Library Implementation*

**License Overview**

All files in this repository fall under the license specified in [COPYING](COPYING). The project is licensed as [AGPL with a lesser clause](https://wiki.unsystem.net/en/index.php/Libbitcoin/License). It may be used within a proprietary project, but the core library and any changes to it must be published online. Source code for this library must always remain free for everybody to access.

**About Libbitcoin**

The libbitcoin toolkit is a set of cross platform C++ libraries for building bitcoin applications. The toolkit consists of several libraries, most of which depend on the foundational [libbitcoin](https://github.com/libbitcoin/libbitcoin) library. Each library's repository can be cloned and built using common [automake](http://www.gnu.org/software/automake) instructions. There are no packages yet in distribution however each library includes an installation script (described below) which is regularly verified in the automated build.

**Table of Contents**

* Installation
  * [Debian/Ubuntu](#debianubuntu)
  * [Macintosh](#macintosh)
  * [Windows](#windows)

## Installation

### Debian/Ubuntu

Libbitcoin requires [GCC 4.8.0](https://gcc.gnu.org/projects/cxx0x.html) minimum.

> For this reason Ubuntu is not supported prior to version 12.04.

To see your GCC version:

```sh
  $ gcc --version
```
If necessary, upgrade your compiler [as follows](http://bit.ly/1vXaaQL):
```sh
  $ sudo apt-get install g++-4.8
  $ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50
  $ sudo update-alternatives --config g++
```
Next install the [build system](http://en.wikipedia.org/wiki/GNU_build_system):
```sh
  $ sudo apt-get install build-essential autoconf automake libtool pkg-config
```
Finally, execute the [install script](https://raw.githubusercontent.com/evoskuil/libbitcoin-consensus/develop/install.sh). This single file will download, build, install and test libbitcoin consensus.
```sh
  $ ./install.sh
```
Libbitcoin is now installed in `/usr/local/`.

#### Notes

If you intend to inspect and/or modify source code you should [git clone](http://git-scm.com/docs/git-clone) libbitcoin consensus and each unpackaged dependency and build them manually. The install script itself is commented so that the manual build steps for each dependency can be inferred by a developer.

You can run the install script from any directory on your system. This will build libbitcoin consensus in a subdirectory named `libbitcoin-consensus_build` and install it to `/usr/local/`. When the build completes successfully the `libbitcoin-consensus_build` directory is deleted.

The install script does not require sudo when using a prefix directory.

The build script clones, builds and installs six unpackaged repositories, namely:

- [bitcoin/secp256k1](https://github.com/bitcoin/secp256k1)
- [libbitcoin/libbitcoin](https://github.com/libbitcoin/libbitcoin)
- [libbitcoin/libbitcoin-consensus](https://github.com/libbitcoin/libbitcoin-consensus)
- [zeromq/libzmq](https://github.com/zeromq/libzmq)
- [zeromq/czmq](https://github.com/zeromq/czmq)
- [zeromq/czmqpp](https://github.com/zeromq/czmqpp)

Of these libraries, only libzmq is packaged. However we require a more recent version of the library in order to take advantage of new features such as the [SOCKS](http://wikipedia.org/wiki/SOCKS) proxy, so we build it as well.

#### Build Options

Any set of `./configure` options can be passed via the install script, for example:

```sh
  $ ./install.sh CPPFLAGS=-DDEBUG CFLAGS="-Og -g"
```

#### Compiling for Testnet

Currently libbitcoin cannot work with both [testnet](https://en.bitcoin.it/wiki/Testnet) and mainnet. This restriction will be lifted in a future version. In order to work with testnet in the interim the libbitcoin libraries must be recompiled with the testnet option:
```sh
  $ ./install.sh --enable-testnet
```

### Macintosh

The OSX installation differs from Linux in the installation of the compiler and packaged dependencies.

To upgrade GCC first set the following environment variables:
```sh
  CC=/usr/local/bin/gcc-4.8
  CXX=/usr/local/bin/g++-4.8
```
Next execute the following commands:
```sh
  $ brew install boost
  $ brew tap homebrew/versions
  $ brew install gcc48
  $ sudo ln -sf /usr/local/bin/g++-4.8 /usr/bin/g++
```
Finally, invoke the install script:
```sh
  $ ./install.sh
```

### Windows

Visual Studio solutions are maintained for all libbitcoin libraries and dependencies.

> The libbitcoin execution environment supports `Windows XP Service Pack 2` and newer.

#### Upgrade Compiler

Libbitcoin requires a C++11 compiler, which means **Visual Studio 2013** minimum. Additionally a pre-release compiler must be installed as an update to Visual Studio. Download and install the following tools as necessary. Both are available free of charge:

* [Visual Studio 2013 Express](http://www.microsoft.com/en-us/download/details.aspx?id=43733)
* [November 2013 CTP Compiler](http://www.microsoft.com/en-us/download/details.aspx?id=41151)

#### Create Local NuGet Repository

Dependencies apart from the libbitcoin libraries are available as [NuGet packages](https://www.nuget.org/packages?q=evoskuil). The libbitcoin solution files are configured with references to these packages. To avoid redundancies these references expect a [NuGet.config](http://docs.nuget.org/docs/release-notes/nuget-2.1) in a central location.

> TODO: provide instructions for creation of the central NuGet repository.

The required set of NuGet packages can be viewed using the [NuGet package manager](http://docs.nuget.org/docs/start-here/managing-nuget-packages-using-the-dialog) from the libbitcoin consensus solution. The NuGet package manager will automatically download missing packages, either from the build scripts or after prompting you in the Visual Studio environment. For your reference these are the required packages:

* Packages maintained by [evoskuil](http://www.nuget.org/profiles/evoskuil)
 * [secp256k1\_vc120](http://www.nuget.org/packages/secp256k1_vc120)

#### Build Libbitcoin Projects

After cloning the the repository the libbitcoin build can be performed manually (from within Visual Studio) or using the `buildall.bat` script provided in the `builds\msvc\build\` subdirectory. The scripts automatically download the required NuGet packages.

> Tip: The `buildall.bat` script builds *all* valid configurations. The build time can be significantly reduced by disabling all but the desired configuration in the `buildbase.bat` of each project.

> The libbitcoin dynamic (DLL) build configurations do not compile, as the exports have not yet been fully implemented. These are currently disabled in the build scripts but you will encounter numerous errors if you build then manually.

#### Optional: Build Everything

The packages above are sourced from GitHub repositories maintained using the same [Visual Studio template](https://github.com/evoskuil/visual-studio-template) as the libbitcoin libraries. If so desired each of these can be built locally, in the same manner as the libbitcoin libraries above. This allows you to avoid using the pre-built NuGet packages. The repositories for each dependency are as follows:

* [evoskuil/secp256k1](https://github.com/evoskuil/secp256k1)

This change is properly accomplished by disabling the "NuGet Dependencies" in the Visual Studio properties user interface and then importing the `.import.props` file(s) for the corresponding dependencies.

> TODO: Update libbitcoin with the .import.props files in a disabled configuration. This will allow this transition to be made entirely in the Visual Studio user interface. Then clarify the above explanation.
