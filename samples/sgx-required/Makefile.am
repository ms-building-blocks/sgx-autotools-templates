## This must come first when building an application that uses Intel
## SGX enclaves.

include $(top_srcdir)/build-aux/sgx_app.am

## It sets the following automake variables:
##
##   AM_CPPFLAGS = -I$(SGXSDK_INCDIR)
##   AM_LDFLAGS = -L$(SGXSDK_LIBDIR)
##
## And a pattern rule for building proxy functions from EDL files:
##
##   %_u.h %_u.c: %.edl
##
## And sets these Makefile variables:
##
##   SGXSDK
##   SGXSDK_BINDIR
##   SGXSDK_INCDIR
##   SGXSDK_LIBDIR
##   SGXSSL
##   SGXSSL_BINDIR
##   SGXSSL_INCDIR
##   SGXSSL_LIBDIR
##   SGX_URTS_LIB
##   SGX_UAE_SERVICE_LIB
##   SGX_EDGER8R

SUBDIRS = EnclaveHash


## Supply additional flags to edger8r here. 
##
## SGX_EDGER8R_FLAGS=


## Needed to make our pattern rule work

EnclaveHash.edl: EnclaveHash/EnclaveHash.edl
	ln -s $?


## Additional automake variables
##
## AM_CPPFLAGS += 
## AM_CFLAGS = 
## AM_CXXFLAGS = 

AM_CPPFLAGS += -fno-builtin-memset

## Additional targets to remove with 'make clean'. You must list
## any edger8r generated files here.

CLEANFILES = EnclaveHash_u.c EnclaveHash_u.h EnclaveHash.edl


## The build target

bin_PROGRAMS = storesecret


## You can't use $(wildcard ...) with automake so all source files 
## have to be explicitly listed.

storesecret_SOURCES = main.c sgx_detect_linux.c sgx_stub.c 
nodist_storesecret_SOURCES = EnclaveHash_u.c EnclaveHash_u.h
BUILT_SOURCES = EnclaveHash_u.c EnclaveHash_u.h

## Library flags. At minimum, an Intel SGX application will need:
##
##   -l$(SGX_URTS_LIB)
##
## Applications that use platform services or perform attestation
## will also need:
##
##  -l$(SGX_UA_SERVICE_LIB)
##
## Use the variables, not the actualy library names to ensure these
## targets work on simulation builds.

storesecret_LDADD=-l$(SGX_URTS_LIB) -ldl -l:libsgx_capable.a -lpthread


