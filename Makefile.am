#
# documentation
#
doc_DATA = README INSTALL COPYING

#
# pkg-config
#
pkgconfig_DATA = libbitcoin-consensus.pc

# look for macros in the m4 subdirectory
ACLOCAL_AMFLAGS = -I m4

#
# headers
#
bitcoin_includedir = ${includedir}/bitcoin
bitcoin_include_HEADERS = \
    include/bitcoin/consensus.hpp

# bitcoin_consensus_includedir = ${includedir}/bitcoin/consensus
# bitcoin_consensus_include_HEADERS = 
#    include/bitcoin/consensus/todo.hpp \

#
# libraries
#
lib_LTLIBRARIES = src/libbitcoin-consensus.la

src_libbitcoin_consensus_la_CPPFLAGS = \
    -I${srcdir}/include \
    ${secp256k1_CFLAGS}

#src_libbitcoin_consensus_la_SOURCES = \
#    src/todo.cpp

src_libbitcoin_client_la_LIBADD = \
    ${secp256k1_LIBS}

