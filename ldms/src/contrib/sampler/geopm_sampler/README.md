GEOPM LDMS SAMPLER PLUGIN
=========================

This directory contains the source, build scripts, and unit tests for
the GEOPM LDMS Sampler Plugin. When enabled, this sampler relies on the
interfaces provided by the GEOPM Service package to read signals. This package
is part of the open source [GEOPM](https://geopm.github.io) project. 

Build Requirements
------------------

The GEOPM LDMS sampler currently requires version 2.0 of the GEOPM
Service library (``libgeopmd.so``).  This library and the corresponding
headers used for compiling the sampler are available as RPM packages
for several Linux distributions or may be built from source.

### Installing RPMs

The GEOPM LDMS sampler **build** requirements are met with the
``libgeopmd0`` and ``geopm-service-devel`` packages. Only the
``libgeopmd0`` package is required when **running** the GEOPM LDMS
sampler. The required version of these packages can be obtained here:
- [libgeopmd0](https://software.opensuse.org/download.html?project=home%3Ageopm%3Arelease-v2.0-candidate&package=libgeopmd0)
- [geopm-service-devel](https://software.opensuse.org/download.html?project=home%3Ageopm%3Arelease-v2.0-candidate&package=geopm-service-devel)

All requirements will be installed in standard locations.

For reference, the instructions for all GEOPM Service packages
(besides ``libgeopmd0`` and ``geopm-service-devel``) can be found
here: [Install Instructions](https://geopm.github.io/install.html)

### Building From Source

The user may optionally build the GEOPM Service package from source.
Please note that when building from source, libraries (e.g.
``libgeopmd.so``) are not installed automatically in standard locations,
so make sure to set ``LD_LIBRARY_PATH`` accordingly when building the
GEOPM LDMS sampler, if need be.


The bash script below shows an example source build that uses the
``v2.0.0+rc1`` release candidate:

    #!/bin/bash
    # Build GEOPM libraries
    GEOPM_URL="https://github.com/geopm/geopm/releases/download"
    GEOPM_RELEASE="/v2.0.0%2Brc1/geopm-service-2.0.0.rc1.tar.gz"
    wget ${GEOPM_URL}${GEOPM_RELEASE}
    tar xvf geopm-service-2.0.0.rc1.tar.gz
    cd geopm-service-2.0.0~rc1/
    GEOPM_PREFIX=$HOME/build/geopm
    # Use configure --help for details on enabling optional accelerator support 
    ./configure --prefix=${GEOPM_PREFIX} --libdir=${GEOPM_PREFIX}/lib64
    make
    make install
    
For reference, the instructions for building different components
of the GEOPM project can be found here: 
[Source Build Instructions](https://geopm.github.io/devel.html#developer-build-process)


OVIS Build
----------

To enable the sampler provide the ``--with-geopm`` option to the configure 
script while building OVIS from source. Please refer to the OVIS documentation 
for general guidance on building the OVIS/LDMS codebase. 


    #!/bin/bash
    # OVIS_SOURCE is the OVIS source directory
    cd $OVIS_SOURCE
    ./configure --with-geopm=${GEOPM_PREFIX}



Using the GEOPM LDMS Sampler
------------------------------

More details on using the sampler can be found on the 
[man page](Plugin_geopm_sampler.man).
