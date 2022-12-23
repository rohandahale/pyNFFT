PyNFFT - Pythonic bindings around the NFFT library
==================================================

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

Installation only for M1 Mac (MacOS > v12.0)
--------------------------------------

Step-by-step installation instructions

#. Install ``fftw``
    #. You need ``gcc`` compiler for installing ``fftw`` with ``--enable-openmp``.  The ``gcc`` in M1 Mac (MacOS > v12.0) actually points to ``clang`` 
    
       Install ``gcc-12`` with brew::
       
            brew install gcc@12
       
    #. Download FFTW 3.3.10 from `fftw.org <http://www.fftw.org/download.html>`_ and extract the folder
    #. ``cd`` into the ``fftw`` folder and using this configuration::
    
            ./configure CC="gcc-12" --enable-shared --enable-threads --enable-openmp
            sudo make
            sudo make check
            sudo make install
            
    #. Check ``/usr/local/lib/`` and ``/usr/local/include/`` to see if ``fftw3`` is installed.
#. Install ``NFFT``
    #. You need ``autoconf automake libtool`` for this step. Install it with::
    
        brew install autoconf automake libtool
        
       Make sure you edit your ``.zshrc`` tp add it your ``PATH``
       
    #. Clone the NFFT git repository::
    
        git clone https://github.com/NFFT/nfft.git
    
    #. ``cd`` into the ``NFFT`` folder and using this configuration::
        
        ./bootstrap.sh
        ./configure CC="gcc-12" --enable-all --enable-openmp --enable-shared --with-fftw3-libdir=/usr/local/lib/ --with-fftw3-includedir=/usr/local/include/
        sudo make
        sudo make check
        sudo make install
        
    #. Check ``/usr/local/lib/`` and ``/usr/local/include/`` to see if ``nfft`` is installed.
    
#. Install ``pyNFFT``
    #. Clone this repository::
        
        git clone 
    
    #. Install ``cython`` with ``pip`` or ``conda`` to run this ``setup.py``::
    
        pip install Cython
        
        or::
        
        conda install -c anaconda cython
        
    #. ``cd`` into pyNFFT folder and build ``pynfft`` from ``setupy.py`` using::
    
        python setup.py build_ext -I /usr/local/include/ -L /usr/local/lib/ -R /usr/local/lib/
        
    #. While being inside the folder, install ``pynfft`` with::
        
        python -m pip install .
        
        or:
        
        pip install .

Usage
-----

See the `tutorial <http://pythonhosted.org/pyNFFT/tutorial.html>`_ 
section of the documentation.


Requirements
------------

- Python 2.7 or greater
- Numpy 1.6 or greater
- NFFT library 3.2 or greater, compiled with openMP support
- Cython 0.12 or greater

Contributing
------------

See the CONTRIBUTING file.

License
-------

The pyNFFT project is licensed under the GPLv3.  See the bundled COPYING file
for more details.
