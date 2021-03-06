.. include:: css.inc

.. _install_ubuntu:


Ubuntu Installation Instructions
################################

.. warning::
    If you want to install the bleeding-edge or development version of Aesara
    from GitHub, please make sure you are reading `the latest version of this
    page <http://deeplearning.net/software/aesara_versions/dev/install_ubuntu.html>`_.

.. |PythonDistRecommended| replace:: The development package (python-dev or python-devel on most Linux distributions) is recommended (see just below)
.. |PlatformCompiler| replace:: ``python-dev``, ``g++`` >= 4.2
.. |CompilerName| replace:: ``g++``

.. include:: requirements.inc

.. include:: install_generic.inc
    :start-line: 5

Prerequisites through System Packages (not recommended)
-------------------------------------------------------

If you want to acquire the requirements through your system packages
and install them system wide follow these instructions:

For Ubuntu 16.04

.. code-block:: bash

    sudo apt-get install python-numpy python-scipy python-dev python-pip python-pytest g++ libopenblas-dev git graphviz
    sudo pip install Aesara

    sudo apt-get install g++-4.9

    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 20
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 10

    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 20
    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 10

    sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 30
    sudo update-alternatives --set cc /usr/bin/gcc

    sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 30
    sudo update-alternatives --set c++ /usr/bin/g++

For Ubuntu 11.10 through 14.04:

.. code-block:: bash

    sudo apt-get install python-numpy python-scipy python-dev python-pip python-pytest g++ libopenblas-dev git

On 14.04, this will install Python 2 by default. If you want to use Python 3:

.. code-block:: bash

    sudo apt-get install python3-numpy python3-scipy python3-dev python3-pip python3-pytest g++ libopenblas-dev git
    sudo pip3 install Aesara

For Ubuntu 11.04:

.. code-block:: bash

    sudo apt-get install python-numpy python-scipy python-dev python-pip python-pytest g++ git libatlas3gf-base libatlas-dev

Manual Openblas installation (deprecated)
-----------------------------------------

The openblas included in some older Ubuntu version is limited to 2
threads. Ubuntu 14.04 do not have this limit. If you want to use more
cores at the same time, you will need to compile it yourself. Here is
some code that will help you.

.. code-block:: bash

    # remove openblas if you installed it
    sudo apt-get remove libopenblas-base
    # Download the development version of OpenBLAS
    git clone git://github.com/xianyi/OpenBLAS
    cd OpenBLAS
    make FC=gfortran
    sudo make PREFIX=/usr/local/ install
    # Tell Aesara to use OpenBLAS.
    # This works only for the current user.
    # Each Aesara user on that computer should run that line.
    echo -e "\n[blas]\nldflags = -lopenblas\n" >> ~/.aesararc
