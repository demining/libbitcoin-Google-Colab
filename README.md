-------------------------
### Run libbitcoin-Google-Colab

https://colab.research.google.com/drive/1OShIMVcFZ_khsUIBOIV1lzrqAGo1gfm_?usp=sharing

-------------------------

All files in this repository fall under the license specified in LICENSE
The project is licensed as AGPL with a lesser clause. It may be used within
a proprietary project, but the core library and any changes to it must be
published online. Source code for this library must always remain free for
everybody to access.

==========================
Debian/Ubuntu Instructions
==========================

Note that you need g++ 4.7 or higher. For this reason Ubuntu 12.04 and older are not supported.

  VVVVVVVVVVV
> Start Here! <
  ^^^^^^^^^^^

  $ sudo apt-get install build-essential autoconf automake libtool libboost-all-dev pkg-config libcurl4-openssl-dev libleveldb-dev libssl-dev
  $ autoreconf -i
  $ ./configure --enable-leveldb
  $ make
  $ sudo make install
  $ sudo ldconfig

libbitcoin is now installed in /usr/local/.

* Ubuntu Precise Pangolin requires libboost1.48-all-dev instead of
  libboost-all-dev above.

--------
Advanced
--------

Files Open Limit
----------------

For the blockchain database, set the max open files limit higher.
The default limit on most Linux systems is too low.

  $ ulimit -n 4096

Core Dependencies
-----------------

You will need:

  - GCC 4.7 or newer
  - Boost 1.48 or newer
  - OpenSSL 0.9 or newer
  - LevelDB

Install Prefix
--------------

'./configure' accepts a --prefix switch. This is useful if you prefer to
install libbitcoin to a local directory instead.

  $ ./configure --enable-leveldb --prefix /home/genjix/usr/
  $ make
  $ make install

Then add these environment variables to the end of your ~/.bashrc to point
software to your local installation. Otherwise software will have trouble
finding the libbitcoin install.

  export LD_LIBRARY_PATH=~/usr/lib/
  export PKG_CONFIG_PATH=~/usr/lib/pkgconfig/

'./configure' also accepts the following flags:
  --enable-testnet (enables the alternative blockchain used for testing)
  --enable-debug   (verbose output)

Compile/Build Flags
-------------------

pkg-config can be invoked to get the neccessary compile and build flags
for creating software using libbitcoin.

  $ pkg-config --cflags --libs libbitcoin

--------
Examples
--------

Start with the examples/ to see a few sample programs:

  $ cd examples/
  $ make
  # Play around with private keys.
  $ ./priv
  # Initialize a new LevelDB blockchain database.
  $ mkdir database
  $ ./initchain database/
  # Run the fullnode example (validates blocks and transactions).
  $ ./fullnode

=======================
Arch Linux Instructions
=======================

Libbitcoin is available from the AUR: https://aur.archlinux.org/packages/libbitcoin-leveldb-git/ 

=======================
Gentoo Linux Instructions
=======================

Libbitcoin is available in the 'bitcoin' overlay. Use layman to fetch
the overlay then emerge as usual.

If you want to use live build, unlock the '**' keyword for net-p2p/libbitcoin
in /etc/portage/package.accept_keywords

====================
Mac OSX Instructions
====================

To build on Mac OSX, you will need to download and compile your own boost,
leveldb using gcc 4.7 before building libbitcoin. Then set the following
environment variables before running the build process.

  CC=/usr/local/bin/gcc-4.7
  CXX=/usr/local/bin/g++-4.7

You will need secp256k1 as a library dependency, if you don't have
it already in your system this is how you get/build/install it from source code.

  $ git clone https://github.com/bitcoin/secp256k1
  $ cd secp256k1
  $ ./autogen.sh
  $ ./configure
  $ make
  $ sudo make install

For Mac OSX Mountain Lion, you need to follow these brew commands:

  $ brew install boost openssl leveldb
  $ brew tap homebrew/versions
  $ brew install gcc48
  # Can be replaced back later if you prefer, but
  # keeping the new g++ is a good idea.
  $ sudo ln -sf /usr/local/bin/g++-4.8 /usr/bin/g++


  $ autoreconf -i
  $ ./configure --enable-leveldb
  $ make
  $ sudo make install


----

|  | Donation Address |
| --- | --- |
| ??? __BTC__ | 1Lw2kh9WzCActXSGHxyypGLkqQZfxDpw8v |
| ??? __ETH__ | 0xaBd66CF90898517573f19184b3297d651f7b90bf |
