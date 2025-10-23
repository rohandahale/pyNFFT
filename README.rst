PyNFFT - Pythonic bindings around the NFFT library (M1/M2/M3/M4 Mac - MacOS16.0)
==================================================================

"The NFFT is a C subroutine library for computing the nonequispaced discrete
Fourier transform (NDFT) in one or more dimensions, of arbitrary input size,
and of complex data."

The `NFFT library <http://www-user.tu-chemnitz.de/~potts/nfft/index.php>`_ is
licensed under GPLv2.

This wrapper provides a somewhat Pythonic access to some of the core NFFT
library functionalities and is largely inspired from the pyFFTW project
developped by Henry Gomersall (http://hgomersall.github.io/pyFFTW/).

The documentation is hosted on `pythonhosted
<http://pythonhosted.org/pyNFFT/>`_, the source code is available on `github
<https://github.com/ghisvail/pyNFFT>`_ and the Python package index page is
`here <https://pypi.python.org/pypi/pyNFFT>`_.

Installation for Apple Silicon Mac (macOS 12.0+, including macOS 16 Sequoia)
-----------------------------------------------------------------------------

Step-by-step installation instructions

#. Install ``fftw``
    #. You need ``gcc`` compiler for installing ``fftw`` with ``--enable-openmp``.  The ``gcc`` in Apple Silicon Mac (macOS > v12.0) actually points to ``clang`` 
    
       Install ``gcc-12`` with brew::
       
            brew install gcc@12
       
    #. Download FFTW 3.3.10 from `fftw.org <http://www.fftw.org/download.html>`_ and extract the folder
    #. ``cd`` into the ``fftw`` folder and use this configuration::
    
            ./configure CC="gcc-12" --enable-shared --enable-threads --enable-openmp
            sudo make
            sudo make check
            sudo make install
            
    #. Check ``/usr/local/lib/`` and ``/usr/local/include/`` to see if ``fftw3`` is installed.
    
#. Install ``NFFT``
    #. You need ``autoconf automake libtool`` for this step. Install it with::
    
        brew install autoconf automake libtool
        
       Make sure you edit your ``.zshrc`` to add it to your ``PATH``

    #. Download the 3.5.3 release of the NFFT git repository::

        https://github.com/NFFT/nfft/releases/download/3.5.3/nfft-3.5.3.tar.gz
    
    #. ``cd`` into the ``NFFT`` folder and use this configuration::
        
        ./bootstrap.sh
        ./configure CC="gcc-12" --enable-all --enable-openmp --enable-shared --with-fftw3-libdir=/usr/local/lib/ --with-fftw3-includedir=/usr/local/include/
        sudo make
        sudo make check
        sudo make install
        
    #. Check ``/usr/local/lib/`` and ``/usr/local/include/`` to see if ``nfft`` is installed.
    
#. Install ``pyNFFT``
    #. Clone this repository::
        
        git clone https://github.com/rohandahale/pyNFFT.git
    
    #. Install ``ehtim``, ``cython`` with ``pip`` to run this ``setup.py``::

        pip install ehtim
        pip install Cython==0.29.32
        
    
    #. ``cd`` into pyNFFT folder, build and install ``pynfft``::
    
        export MACOSX_DEPLOYMENT_TARGET=16.0
        pip install -e . --no-build-isolation
    
    #. **Important:** Fix the duplicate RPATH issue that may occur with conda/micromamba environments.
    
       Find your Python environment path and run::
        
        # Replace YOUR_USERNAME and YOUR_ENV_NAME with your actual values
        for module in nfft solver util; do
            install_name_tool -delete_rpath /Users/YOUR_USERNAME/path/to/envs/YOUR_ENV_NAME/lib \
                pynfft/${module}.cpython-311-darwin.so
            install_name_tool -add_rpath /usr/local/lib \
                pynfft/${module}.cpython-311-darwin.so
        done
    
    #. Verify the installation::
    
        python
        >>> import pynfft
        >>> print(pynfft.__version__)
    
    #. Done.

**Note for macOS 16 (Sequoia) users:** The setup.py has been updated to handle the macOS 16.0 deployment target requirements. If you're using an older macOS version, you can adjust the ``minos`` value in the setup.py accordingly (e.g., 12.0, 13.0, etc.).

Usage
-----

See the `tutorial <http://pythonhosted.org/pyNFFT/tutorial.html>`_ 
section of the documentation.


Recommended versions
------------

- Python 3.11
- ehtim 1.2.10
- FFTW 3.3.10
- NFFT 3.5.3
- Cython 0.29.32

Contributing
------------

See the CONTRIBUTING file.

License
-------

The pyNFFT project is licensed under the GPLv3.  See the bundled COPYING file
for more details.