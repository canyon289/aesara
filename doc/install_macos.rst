.. include:: css.inc

.. _install_macos:


Mac OS Installation Instructions
################################

There are various ways to install Aesara dependencies on a Mac. Here
we describe the process in detail with Anaconda, Homebrew or MacPorts
but if you did it differently and it worked, please let us know the
details so that we can add alternative instructions.

.. |PythonDistRecommended| replace:: The conda distribution is highly recommended
.. |PlatformCompiler| replace:: ``clang`` (the system version)
.. |CompilerName| replace:: ``Clang``

.. include:: requirements.inc

.. attention::

    Aesara officially supports only clang on OS X.  This can be installed
    by getting XCode from the App Store and running it once to install the
    command-line tools.

.. include:: install_generic.inc
    :start-line: 5

Requirements through Homebrew (not recommended)
-----------------------------------------------

Install python with homebrew:

.. code-block:: bash

    $ brew install python # or python3 if you prefer

This will install pip.  Then use pip to install numpy, scipy:

.. code-block:: bash

    $ pip install numpy scipy

If you want to use openblas instead of Accelerate, you have to install
numpy and scipy with hombrew:

.. code-block:: bash

    $ brew tap homebrew/python
    $ brew install numpy --with-openblas
    $ brew install scipy --with-openblas


Requirements through MacPorts (not recommended)
-----------------------------------------------

Using `MacPorts <http://www.macports.org/>`__ to install all required
Aesara dependencies is easy, but be aware that it will take a long time
(a few hours) to build and install everything.

- MacPorts requires installing XCode first (which can be found in the
  Mac App Store), if you do not have it already.
  If you can't install it from the App Store, look in your MacOS X installation
  DVD for an old version. Then update your Mac to update XCode.

- Download and install `MacPorts <http://www.macports.org/>`__, then
  ensure its package list is up-to-date with ``sudo port selfupdate``.

- Then, in order to install one or more of the required libraries, use
  ``port install``, e.g. as follows:

    .. code-block:: bash

        $ sudo port install py27-numpy +atlas py27-scipy +atlas py27-pip

  This will install all the required Aesara dependencies. gcc will
  be automatically installed (since it is a SciPy dependency), but be
  aware that it takes a long time to compile (hours)!
  Having NumPy and SciPy linked with ATLAS (an optimized BLAS
  implementation) is not mandatory, but recommended if you care about
  performance.

- You might have some different versions of gcc, SciPy, NumPy, Python installed
  on your system, perhaps via Xcode. It is a good idea to use **either** the
  MacPorts version of everything **or** some other set of compatible versions
  (e.g. provided by Xcode or Fink). The advantages of MacPorts are the
  transparency with which everything can be installed and the fact that
  packages are updated quite frequently. The following steps describe how to
  make sure you are using the MacPorts version of these packages.

- In order to use the MacPorts version of Python, you will probably
  need to explicitly select it with ``sudo port select python python27``. The
  reason this is necessary is because you may have an Apple-provided Python
  (via, for example, an Xcode installation). After performing this step, you
  should check that the symbolic link provided by ``which python`` points to
  the MacPorts python. For instance, on MacOS X Lion with MacPorts 2.0.3,
  the output of ``which python`` is ``/opt/local/bin/python`` and this symbolic
  link points to ``/opt/local/bin/python2.7``. When executing ``sudo
  port select python python27-apple`` (which you should **not** do), the link
  points to ``/usr/bin/python2.7``.

- Similarly, make sure that you are using the MacPorts-provided gcc:
  use ``sudo port select gcc`` to see which gcc installs you have on the
  system. Then execute for instance ``sudo port select gcc mp-gcc44``
  to create a symlink that points to the correct (MacPorts) gcc (version 4.4
  in this case).

- At this point, if you have not done so already, it may be a good idea to
  close and restart your terminal, to make sure all configuration changes
  are properly taken into account.

- Afterwards, please check that the ``scipy`` module that is imported in
  Python is the right one (and is a recent one). For instance, ``import
  scipy`` followed by ``print scipy.__version__`` and ``print scipy.__path__``
  should result in a version number of at least 0.7.0 and a path that starts
  with ``/opt/local`` (the path where MacPorts installs its packages). If this
  is not the case, then you might have some old installation of ``scipy`` in your
  ``PYTHONPATH`` so you should edit ``PYTHONPATH`` accordingly.

- Please follow the same procedure with ``numpy``.

- This is covered in the MacPorts installation process, but make sure that
  your ``PATH`` environment variable contains ``/opt/local/bin`` and
  ``/opt/local/sbin`` before any other paths (to ensure that the Python and
  gcc binaries that you installed with MacPorts are visible first).

- MacPorts does not automatically create ``pip`` symlinks pointing to the
  MacPorts version; you can add them yourself with

    .. code-block:: bash

        $ sudo ln -s /opt/local/bin/pip-2.7 /opt/local/bin/pip
