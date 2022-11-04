# Toolchains

## Overview

A **toolchain** on a TAMU HPRC cluster is a collection of tools used for
building software. They typically include:

  - a compiler collection providing basic language support
    (C/Fortran/C++)
  - a MPI implementation for multi-node communication
  - a set of linear algebra libraries (FFTW/BLAS/LAPACK) for accelerated
    math

Most modules on our clusters include the toolchain that was used to
build them in their version tag (e.g. .Python/3.5.2-intel-2016b was
built with the intel/2016b toolchain below).

Mixing components from different toolchains almost always leads to
problems. For example, if you mix Intel MPI modules with OpenMPI modules
you can guarantee your program will not run (even if you manage to get
it to compile). We recommend you always use modules from the same
(sub)toolchains. \[Since late 2016 we've been looking at EasyBuild's
--minimal-toolchain option to cut down on module count, so "GCCcore" is
now a common new "subtoolchain"\]

## Currently Supported

<table>
<thead>
<tr class="header">
<th><p>Toolchain</p></th>
<th><p>Compiler(s)</p></th>
<th><p>MPI</p></th>
<th><p>Linear Algebra</p></th>
<th><p>Available on:</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
<td><p>binutils</p></td>
<td><p>GCC(core)</p></td>
<td><p>Intel Compilers<br />
(iccifort)</p></td>
<td><p>Intel MPI<br />
(impi)</p></td>
</tr>
<tr class="even">
<td><p>intel</p></td>
<td><p>Composed of the Intel Cluster Toolkit built upon a particular version of GCC. These are the recommended toolchains for HPRC Intel-based clusters.</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>2020b</p></td>
<td><p>2.35</p></td>
<td><p>10.2.0</p></td>
<td><p>2020.4.304</p></td>
<td><p>2019.9.304</p></td>
</tr>
<tr class="even">
<td><p>2020a</p></td>
<td><p>2.34</p></td>
<td><p>9.3.0</p></td>
<td><p>2020.1.217</p></td>
<td><p>2019.7.217</p></td>
</tr>
<tr class="odd">
<td><p>2019b</p></td>
<td><p>2.32</p></td>
<td><p>8.3.0</p></td>
<td><p>2019.5.281</p></td>
<td><p>2018.5.288</p></td>
</tr>
<tr class="even">
<td><p>2019a</p></td>
<td><p>2.31</p></td>
<td><p>8.2.0</p></td>
<td><p>2019.1.144</p></td>
<td><p>2018.4.274</p></td>
</tr>
<tr class="odd">
<td><p>2018b</p></td>
<td><p>2.30</p></td>
<td><p>7.3.0</p></td>
<td><p>2018.3.222</p></td>
<td><p>2018.3.222</p></td>
</tr>
<tr class="even">
<td><p>2018a</p></td>
<td><p>2.28</p></td>
<td><p>6.4.0</p></td>
<td><p>2018.1.163</p></td>
<td><p>2018.1.163</p></td>
</tr>
<tr class="odd">
<td><p>2017b</p></td>
<td><p>2.28</p></td>
<td><p>6.4.0</p></td>
<td><p>2017.4.196</p></td>
<td><p>2017.3.196</p></td>
</tr>
<tr class="even">
<td><p>2017A</p></td>
<td><p>2.2x (system)</p></td>
<td><p>6.3.0</p></td>
<td><p>2017.1.132</p></td>
<td><p>2017.1.132</p></td>
</tr>
<tr class="odd">
<td><p>2016b</p></td>
<td><p>2.26</p></td>
<td><p>5.4.0</p></td>
<td><p>2016.3.210</p></td>
<td><p>5.1.3.181</p></td>
</tr>
<tr class="even">
<td><p>2016a</p></td>
<td><p>2.25</p></td>
<td><p>4.9.3</p></td>
<td><p>2016.1.150</p></td>
<td><p>5.1.2.150</p></td>
</tr>
<tr class="odd">
<td><p>2015B</p></td>
<td><p>2.2x (system)</p></td>
<td><p>4.8.4</p></td>
<td><p>2015.3.187</p></td>
<td><p>5.0.3.048</p></td>
</tr>
<tr class="even">
<td><p>iomkl</p></td>
<td><p>A combination of the Intel compiler and math kernel library components with OpenMPI.</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>2020a</p></td>
<td><p>2.34</p></td>
<td><p>9.3.0</p></td>
<td><p>2020.1.217</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2019.01</p></td>
<td><p>2.31</p></td>
<td><p>8.2.0</p></td>
<td><p>2019.1.144</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2018b</p></td>
<td><p>2.30</p></td>
<td><p>7.3.0</p></td>
<td><p>2018.3.222</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2018a</p></td>
<td><p>2.28</p></td>
<td><p>6.4.0</p></td>
<td><p>2018.1.163</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2017b</p></td>
<td><p>2.28</p></td>
<td><p>6.4.0</p></td>
<td><p>2017.4.196</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2017A</p></td>
<td><p>2.2x (system)</p></td>
<td><p>6.3.0</p></td>
<td><p>2017.1.132</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2016.07</p></td>
<td><p>2.26</p></td>
<td><p>5.4.0</p></td>
<td><p>2016.3.210</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2015B</p></td>
<td><p>2.2x (system)</p></td>
<td><p>4.8.4</p></td>
<td><p>2015.3.187</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>foss</p></td>
<td><p>Based upon "Free and Open-Source Software". These toolchains produce slightly slower code but do provide code portability to other platforms (e.g. those that don't have an Intel compiler).</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>2020b</p></td>
<td><p>2.35</p></td>
<td><p>10.2.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2020a</p></td>
<td><p>2.34</p></td>
<td><p>9.3.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2019b</p></td>
<td><p>2.32</p></td>
<td><p>8.3.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2019a</p></td>
<td><p>2.31</p></td>
<td><p>8.2.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2018b</p></td>
<td><p>2.30</p></td>
<td><p>7.3.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2018a</p></td>
<td><p>2.28</p></td>
<td><p>6.4.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2017b</p></td>
<td><p>2.28</p></td>
<td><p>6.4.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2017A</p></td>
<td><p>2.2x (system)</p></td>
<td><p>6.3.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2016b</p></td>
<td><p>2.26</p></td>
<td><p>5.4.0</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2016a</p></td>
<td><p>2.25</p></td>
<td><p>4.9.3</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="even">
<td><p>2015b</p></td>
<td><p>2.25</p></td>
<td><p>4.9.3</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
<tr class="odd">
<td><p>2015a</p></td>
<td><p>2.2x (system)</p></td>
<td><p>4.9.2</p></td>
<td><p>-</p></td>
<td><p>-</p></td>
</tr>
</tbody>
</table>

1.  Two new/additional toolchains, **goolfc** and **fosscuda** are
    essentially the **foss** toolchain with [OpenMPI compiled with
    support for CUDA](https://www.open-mpi.org/faq/?category=buildcuda)
    (9.0.176. for 2017b).
2.  For details on using Intel MKL's BLAS and ScaLAPACK (and at some
    point FFTW), see [ our current Intel MKL page](/kb3/Software/Intel-Cluster-Suite/Math-Kernel-Library/SW@MKL/ "wikilink").
    Also see [ the **buildenv**
    modules](/kb3/Software/useful-tools/SW@Toolchains/#the-buildenv-modules "wikilink") section
    below for a number of useful environment variables when building
    with different toolchains.
3.  Note: OpenMPI 1.10.x is largely incompatible with all previous and
    later versions and should probably be avoided.

## Our recommended toolchains

  - In general, we recommend the **intel** toolchain with Intel
    compilers, MPI and linear algebra (MKL) for the best performance on
    HPRC clusters.
  - In many cases, using **icc** instead of **gcc** takes a lot of
    effort so you may find things easier with the **foss** toolchain.
  - As of August 2021, the new recommended suite is the **2020b** suite.
    Older versions may have more modules available and newer ones might
    offer some bug fixes and speedups, but for now we recommend
    **2020b** (e.g. **intel/2020b**).

## Older, but still relevant, information

### A breakdown of our 2017A toolchains

For the past few years, TAMU HPRC has been using
[EasyBuild](http://easybuild.readthedocs.io/en/latest/index.html) to
deploy commonly used HPC libraries. In the past we've tried to use what
EasyBuild contributors (who have HPC systems of their own) use/deploy as
a guide for software deployment. For 2017A, we've set off on a new path.

With the recent addition of the **--minimal-toolchain** option, which
allows us to minimize the overall module count and share common modules
among many toolchains, we've tried to trim things down. Additionally, in
an attempt to keep as closely aligned with the the Linux distribution in
use, we've deferred to many of the distribution-provided build tools
like **autoconf/automake/binutils/cmake/make/libtool/pkgconfig**/etc.

As such, the modules in the 2017A toolchain aren't as easy to determine
what works with what.

#### Components by version suffix

  - **-GCCcore-6.3.0** - these were buit with **gcc** 6.3.0 using the
    system **binutils** (which is a deviation from how EasyBuild does it
    but we thought best to try here).
  - **-GCCcore-6.3.0-Python-2.7.12-bare** - these were built with the
    most basic of Python (only what was required) but do not include a
    proper Python module. If you use these, you must load a Python based
    on a full toolchain (intel/iomkl/foss). IF you don't load a full
    Python module and attempt to use these with the system python, THEN
    it will likely fail.
  - **-iimpi/iompi/gompi-2017A** - these are packages that required MPI,
    but didn't necessarily require linear algebra packages like MKL or
    BLAS/FFTW/LAPACK. These are useful if you want to, for example, use
    the Intel compilers and MPI but want to use the non-MKL FFTW.
    \[Note: The first letter, 'i' or 'g', indicates whether the compiler
    was Intel or GCC. The second letter, 'i' or 'o' indicates whether
    the MPI was Intel or OpenMPI.\]
  - **-intel/iomkl/foss-2017A** - these are the full blown toolchains
    with compilers/MPI/math. See the table above for details.

There may be variations on that in the future. But that covers most of
2017A for now.

#### Motivations

1.  **minimizing module count** - for example, it makes no sense to have
    three versions of **bzip2** (intel/iomkl/foss) when a single version
    built with GCC can be used for all.
2.  **more closely aligning with Linux distribution provided build
    tools** - in addition to the above, we wanted to make sure core
    utilities like **binutils** were well suited for the C library
    (**glibc**) installed on the cluster involved. Beyond that, we found
    that in most cases, the provided build tools like
    **autoconf/automake/cmake/make/libtool/pkgconfig** were sufficient,
    we tried to use the system-provided ones where possible. We also use
    the system-provided **openssl-devel** (for timely security updates)
    and **zlib-devel** (which is required by **openssl-devel**).

#### Deficiencies

  - by relying upon the system **binutils**, we were:
      - unable to fully use AVX2 and AVX512 vector extensions.
      - unable to build certain programs due to missing tools provided
        by newer **binutils**

### Older notes on 2017b toolchains

Other than newer versions, the breakdown for 2017b is similar to 2017A.
Key differences include:

  - using an updated version of binutils. For 2017A, we went with the
    system binutils in order to eliminate it as the cause of some of the
    problems we were having on terra. It turned out not to be a factor.
    However, we also found that it precluded us from taking advantage of
    such features like AVX2 (and AVX512) on terra. So we've gone back to
    using the binutils recommended upstream by the EasyBuild people.
  - unfortunately the "Python-bare" packages are much less prevalent.
    The motivation for this was to reduce the total number of modules.
    For example, there is no reason to build an intel, iomkl and foss
    version of YAML when the GCCcore version would work for all three.
    However, we've not had much luck convincing the upstream that the
    -bare option is either viable (which we've demonstrated it is) or
    clear to users (they have a point there... there has certainly been
    confusion at times with 2017A). So, for the most part, you won't see
    as many Python-bare packages this time around (though there are
    still a few).

## Others

In the past, we've offered different combinations including some that
use the Portland Groups compilers and some that use different variants
of MPI (e.g. MVAPICH, MPICH, MPICH2). If the need arises to build such
toolchains in the future, we will consider it. But for now, users are
recommended to use one of the toolchains above (preferably the most
recent).

## The **buildenv** modules

For each toolchain above there exists a **buildenv** module that:

1.  loads the toolchain
2.  sets a number of useful flags used when compiling/linking programs
    with that toolchain

### Examples

For example, here is what **buildenv** provides for a couple of our
current toolchains.

#### intel/2017b

    $ ml -t show buildenv/default-intel-2017b
    ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       /sw/eb/mods/all/buildenv/default-intel-2017b.lua:
    ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    help([[
    Description
    ===========
    This module sets a group of environment variables for compilers, linkers,
     maths libraries, etc., that you can use to easily transition between
     toolchains when building your software. To query the variables being set
     please use: module show <this module name>
    
    
    More information
    ================
     - Homepage: None
    ]])
    whatis("Description: 
     This module sets a group of environment variables for compilers, linkers,
     maths libraries, etc., that you can use to easily transition between
     toolchains when building your software. To query the variables being set
     please use: module show <this module name>
    ")
    whatis("Homepage: None")
    conflict("buildenv")
    load("intel/2017b")
    setenv("EBROOTBUILDENV","/sw/eb/sw/buildenv/default-intel-2017b")
    setenv("EBVERSIONBUILDENV","default")
    setenv("EBDEVELBUILDENV","/sw/eb/sw/buildenv/default-intel-2017b/easybuild/buildenv-default-intel-2017b-easybuild-devel")
    setenv("BLACS_INC_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include")
    setenv("BLACS_LIB_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64")
    setenv("BLACS_MT_STATIC_LIBS","libmkl_blacs_intelmpi_lp64.a")
    setenv("BLACS_STATIC_LIBS","libmkl_blacs_intelmpi_lp64.a")
    setenv("BLAS_INC_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include")
    setenv("BLAS_LAPACK_INC_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include")
    setenv("BLAS_LAPACK_LIB_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64")
    setenv("BLAS_LAPACK_MT_STATIC_LIBS","libmkl_intel_lp64.a,libmkl_intel_thread.a,libmkl_core.a,libiomp5.a,libpthread.a")
    setenv("BLAS_LAPACK_STATIC_LIBS","libmkl_intel_lp64.a,libmkl_sequential.a,libmkl_core.a")
    setenv("BLAS_LIB_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64")
    setenv("BLAS_MT_STATIC_LIBS","libmkl_intel_lp64.a,libmkl_intel_thread.a,libmkl_core.a,libiomp5.a,libpthread.a")
    setenv("BLAS_STATIC_LIBS","libmkl_intel_lp64.a,libmkl_sequential.a,libmkl_core.a")
    setenv("CC","icc")
    setenv("CFLAGS","-O2 -xHost -ftz -fp-speculation=safe -fp-model source")
    setenv("CPPFLAGS","-I/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include")
    setenv("CXX","icpc")
    setenv("CXXFLAGS","-O2 -xHost -ftz -fp-speculation=safe -fp-model source")
    setenv("F77","ifort")
    setenv("F90","ifort")
    setenv("F90FLAGS","-O2 -xHost -ftz -fp-speculation=safe -fp-model source")
    setenv("FC","ifort")
    setenv("FCFLAGS","-O2 -xHost -ftz -fp-speculation=safe -fp-model source")
    setenv("FFLAGS","-O2 -xHost -ftz -fp-speculation=safe -fp-model source")
    setenv("FFTW_INC_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include/fftw")
    setenv("FFTW_LIB_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64")
    setenv("FFTW_STATIC_LIBS","libfftw3xc_intel.a,libmkl_intel_lp64.a,libmkl_sequential.a,libmkl_core.a")
    setenv("FFTW_STATIC_LIBS_MT","-fftw3xc_intel -mkl_intel_lp64 -mkl_sequential -mkl_core")
    setenv("FFT_INC_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include/fftw")
    setenv("FFT_LIB_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64")
    setenv("FFT_STATIC_LIBS","libfftw3xc_intel.a,libmkl_intel_lp64.a,libmkl_sequential.a,libmkl_core.a")
    setenv("FFT_STATIC_LIBS_MT","libfftw3xc_intel.a,libmkl_intel_lp64.a,libmkl_sequential.a,libmkl_core.a")
    setenv("I_MPI_CC","icc")
    setenv("I_MPI_CXX","icpc")
    setenv("I_MPI_F77","ifort")
    setenv("I_MPI_F90","ifort")
    setenv("I_MPI_FC","ifort")
    setenv("LAPACK_INC_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include")
    setenv("LAPACK_LIB_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64")
    setenv("LAPACK_MT_STATIC_LIBS","libmkl_intel_lp64.a,libmkl_intel_thread.a,libmkl_core.a,libiomp5.a,libpthread.a")
    setenv("LAPACK_STATIC_LIBS","libmkl_intel_lp64.a,libmkl_sequential.a,libmkl_core.a")
    setenv("LDFLAGS","-L/sw/eb/sw/icc/2017.4.196-GCC-6.4.0-2.28/lib/intel64 -L/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/lib -L/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64 -L/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/lib")
    setenv("LIBBLACS","-Wl,-Bstatic -Wl,--start-group -lmkl_blacs_intelmpi_lp64 -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBBLACS_MT","-Wl,-Bstatic -Wl,--start-group -lmkl_blacs_intelmpi_lp64 -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBBLAS","-Wl,-Bstatic -Wl,--start-group -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBBLAS_MT","-Wl,-Bstatic -Wl,--start-group -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -Wl,--end-group -Wl,-Bdynamic -liomp5 -lpthread")
    setenv("LIBFFT","-Wl,-Bstatic -Wl,--start-group -lfftw3xc_intel -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBFFT_MT","-Wl,-Bstatic -Wl,--start-group -lfftw3xc_intel -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBLAPACK","-Wl,-Bstatic -Wl,--start-group -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBLAPACK_MT","-Wl,-Bstatic -Wl,--start-group -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -Wl,--end-group -Wl,-Bdynamic -liomp5 -lpthread")
    setenv("LIBLAPACK_MT_ONLY","-Wl,-Bstatic -Wl,--start-group -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -Wl,--end-group -Wl,-Bdynamic -liomp5 -lpthread")
    setenv("LIBLAPACK_ONLY","-Wl,-Bstatic -Wl,--start-group -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBS","-liomp5 -lpthread")
    setenv("LIBSCALAPACK","-Wl,-Bstatic -Wl,--start-group -lmkl_scalapack_lp64 -lmkl_blacs_intelmpi_lp64 -lmkl_intel_lp64 -lmkl_sequential -lmkl_core -Wl,--end-group -Wl,-Bdynamic")
    setenv("LIBSCALAPACK_MT","-Wl,-Bstatic -Wl,--start-group -lmkl_scalapack_lp64 -lmkl_blacs_intelmpi_lp64 -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -Wl,--end-group -Wl,-Bdynamic -liomp5 -lpthread")
    setenv("LIBSCALAPACK_MT_ONLY","-Wl,-Bstatic -Wl,--start-group -lmkl_scalapack_lp64 -Wl,--end-group -Wl,-Bdynamic -liomp5 -lpthread")
    setenv("LIBSCALAPACK_ONLY","-Wl,-Bstatic -Wl,--start-group -lmkl_scalapack_lp64 -Wl,--end-group -Wl,-Bdynamic")
    setenv("MPICC","mpiicc")
    setenv("MPICH_CC","icc")
    setenv("MPICH_CXX","icpc")
    setenv("MPICH_F77","ifort")
    setenv("MPICH_F90","ifort")
    setenv("MPICH_FC","ifort")
    setenv("MPICXX","mpiicpc")
    setenv("MPIF77","mpiifort")
    setenv("MPIF90","mpiifort")
    setenv("MPIFC","mpiifort")
    setenv("MPI_INC_DIR","/sw/eb/sw/impi/2017.3.196-iccifort-2017.4.196-GCC-6.4.0-2.28/include64")
    setenv("MPI_LIB_DIR","/sw/eb/sw/impi/2017.3.196-iccifort-2017.4.196-GCC-6.4.0-2.28/lib64")
    setenv("MPI_LIB_SHARED","/sw/eb/sw/impi/2017.3.196-iccifort-2017.4.196-GCC-6.4.0-2.28/lib64/libmpi.so")
    setenv("MPI_LIB_STATIC","/sw/eb/sw/impi/2017.3.196-iccifort-2017.4.196-GCC-6.4.0-2.28/lib64/libmpi.a")
    setenv("OPTFLAGS","-O2 -xHost")
    setenv("PRECFLAGS","-ftz -fp-speculation=safe -fp-model source")
    setenv("SCALAPACK_INC_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/include")
    setenv("SCALAPACK_LIB_DIR","/sw/eb/sw/imkl/2017.3.196-iimpi-2017b/mkl/lib/intel64")
    setenv("SCALAPACK_MT_STATIC_LIBS","libmkl_scalapack_lp64.a,libmkl_blacs_intelmpi_lp64.a,libmkl_intel_lp64.a,libmkl_intel_thread.a,libmkl_core.a,libiomp5.a,libpthread.a")
    setenv("SCALAPACK_STATIC_LIBS","libmkl_scalapack_lp64.a,libmkl_blacs_intelmpi_lp64.a,libmkl_intel_lp64.a,libmkl_sequential.a,libmkl_core.a")

#### foss/2018a

    $ ml -t show buildenv/default-foss-2018a
    ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       /sw/eb/mods/all/buildenv/default-foss-2018a.lua:
    ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    help([[
    Description
    ===========
    This module sets a group of environment variables for compilers, linkers,
     maths libraries, etc., that you can use to easily transition between
     toolchains when building your software. To query the variables being set
     please use: module show <this module name>
    
    
    More information
    ================
     - Homepage: None
    ]])
    whatis("Description: 
     This module sets a group of environment variables for compilers, linkers,
     maths libraries, etc., that you can use to easily transition between
     toolchains when building your software. To query the variables being set
     please use: module show <this module name>
    ")
    whatis("Homepage: None")
    conflict("buildenv")
    load("foss/2018a")
    setenv("EBROOTBUILDENV","/sw/eb/sw/buildenv/default-foss-2018a")
    setenv("EBVERSIONBUILDENV","default")
    setenv("EBDEVELBUILDENV","/sw/eb/sw/buildenv/default-foss-2018a/easybuild/buildenv-default-foss-2018a-easybuild-devel")
    setenv("BLAS_INC_DIR","/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/include")
    setenv("BLAS_LAPACK_INC_DIR","/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/include")
    setenv("BLAS_LAPACK_LIB_DIR","/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/lib")
    setenv("BLAS_LAPACK_MT_STATIC_LIBS","libopenblas.a,libgfortran.a")
    setenv("BLAS_LAPACK_STATIC_LIBS","libopenblas.a,libgfortran.a")
    setenv("BLAS_LIB_DIR","/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/lib")
    setenv("BLAS_MT_STATIC_LIBS","libopenblas.a,libgfortran.a")
    setenv("BLAS_STATIC_LIBS","libopenblas.a,libgfortran.a")
    setenv("CC","gcc")
    setenv("CFLAGS","-O2 -ftree-vectorize -march=native -fno-math-errno")
    setenv("CPPFLAGS","-I/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/include -I/sw/eb/sw/ScaLAPACK/2.0.2-gompi-2018a-OpenBLAS-0.2.20/include -I/sw/eb/sw/FFTW/3.3.7-gompi-2018a/include")
    setenv("CXX","g++")
    setenv("CXXFLAGS","-O2 -ftree-vectorize -march=native -fno-math-errno")
    setenv("F77","gfortran")
    setenv("F90","gfortran")
    setenv("F90FLAGS","-O2 -ftree-vectorize -march=native -fno-math-errno")
    setenv("FC","gfortran")
    setenv("FCFLAGS","-O2 -ftree-vectorize -march=native -fno-math-errno")
    setenv("FFLAGS","-O2 -ftree-vectorize -march=native -fno-math-errno")
    setenv("FFTW_INC_DIR","/sw/eb/sw/FFTW/3.3.7-gompi-2018a/include")
    setenv("FFTW_LIB_DIR","/sw/eb/sw/FFTW/3.3.7-gompi-2018a/lib")
    setenv("FFTW_STATIC_LIBS","libfftw3.a")
    setenv("FFTW_STATIC_LIBS_MT","-fftw3 -pthread")
    setenv("FFT_INC_DIR","/sw/eb/sw/FFTW/3.3.7-gompi-2018a/include")
    setenv("FFT_LIB_DIR","/sw/eb/sw/FFTW/3.3.7-gompi-2018a/lib")
    setenv("FFT_STATIC_LIBS","libfftw3.a")
    setenv("FFT_STATIC_LIBS_MT","libfftw3.a,libpthread.a")
    setenv("FLIBS","-lgfortran")
    setenv("LAPACK_INC_DIR","/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/include")
    setenv("LAPACK_LIB_DIR","/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/lib")
    setenv("LAPACK_MT_STATIC_LIBS","libopenblas.a,libgfortran.a")
    setenv("LAPACK_STATIC_LIBS","libopenblas.a,libgfortran.a")
    setenv("LDFLAGS","-L/sw/eb/sw/GCCcore/6.4.0/lib64 -L/sw/eb/sw/GCCcore/6.4.0/lib -L/sw/eb/sw/OpenBLAS/0.2.20-GCC-6.4.0-2.28/lib -L/sw/eb/sw/ScaLAPACK/2.0.2-gompi-2018a-OpenBLAS-0.2.20/lib -L/sw/eb/sw/FFTW/3.3.7-gompi-2018a/lib")
    setenv("LIBBLAS","-lopenblas -lgfortran")
    setenv("LIBBLAS_MT","-lopenblas -lgfortran")
    setenv("LIBFFT","-lfftw3")
    setenv("LIBFFT_MT","-lfftw3 -lpthread")
    setenv("LIBLAPACK","-lopenblas -lgfortran")
    setenv("LIBLAPACK_MT","-lopenblas -lgfortran")
    setenv("LIBLAPACK_MT_ONLY","-lopenblas -lgfortran")
    setenv("LIBLAPACK_ONLY","-lopenblas -lgfortran")
    setenv("LIBS","-lm -lpthread")
    setenv("LIBSCALAPACK","-lscalapack -lopenblas -lgfortran")
    setenv("LIBSCALAPACK_MT","-lscalapack -lopenblas -lpthread -lgfortran")
    setenv("LIBSCALAPACK_MT_ONLY","-lscalapack -lgfortran")
    setenv("LIBSCALAPACK_ONLY","-lscalapack -lgfortran")
    setenv("MPICC","mpicc")
    setenv("MPICXX","mpicxx")
    setenv("MPIF77","mpifort")
    setenv("MPIF90","mpifort")
    setenv("MPIFC","mpifort")
    setenv("MPI_INC_DIR","/sw/eb/sw/OpenMPI/2.1.2-GCC-6.4.0-2.28/include")
    setenv("MPI_LIB_DIR","/sw/eb/sw/OpenMPI/2.1.2-GCC-6.4.0-2.28/lib")
    setenv("MPI_LIB_SHARED","/sw/eb/sw/OpenMPI/2.1.2-GCC-6.4.0-2.28/lib/libmpi.so")
    setenv("MPI_LIB_STATIC","")
    setenv("OMPI_CC","gcc")
    setenv("OMPI_CXX","g++")
    setenv("OMPI_F77","gfortran")
    setenv("OMPI_F90","gfortran")
    setenv("OMPI_FC","gfortran")
    setenv("OPTFLAGS","-O2 -ftree-vectorize -march=native")
    setenv("PRECFLAGS","-fno-math-errno")
    setenv("SCALAPACK_INC_DIR","/sw/eb/sw/ScaLAPACK/2.0.2-gompi-2018a-OpenBLAS-0.2.20/include")
    setenv("SCALAPACK_LIB_DIR","/sw/eb/sw/ScaLAPACK/2.0.2-gompi-2018a-OpenBLAS-0.2.20/lib")
    setenv("SCALAPACK_MT_STATIC_LIBS","libscalapack.a,libopenblas.a,libgfortran.a,libpthread.a")
    setenv("SCALAPACK_STATIC_LIBS","libscalapack.a,libopenblas.a,libgfortran.a")
