.. include:: css.inc

.. _install_windows:


Windows Installation Instructions
#################################

.. warning::
    If you want to install the bleeding-edge or development version of Aesara
    from GitHub, please make sure you are reading `the latest version of this
    page <http://deeplearning.net/software/aesara_versions/dev/install_windows.html>`_.

.. |PythonDistRecommended| replace:: The conda distribution is highly recommended
.. |PlatformCompiler| replace:: GCC compiler with ``g++`` (version >= ``4.2.*``), and Python development files
.. |CompilerName| replace:: ``g++``

.. List of requirements, optional requirements, and installation of miniconda.
.. include:: requirements.inc
    :end-before: .. install_requirements_and_optional_packages

Install requirements and optional packages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

    conda install numpy scipy mkl-service libpython <m2w64-toolchain> pytest <sphinx> <pydot-ng> <git>

.. note::

    * Arguments between <...> are optional.
    * ``m2w64-toolchain`` package provides a fully-compatible version of GCC and is then highly recommended.
    * ``git`` package installs git source control through conda, which is required for the development version of Aesara


.. Installation of Aesara.
.. include:: install_generic.inc
    :start-after: .. _install_generic:

Instructions for other Python distributions (not recommended)
=============================================================

If you plan to use Aesara with other Python distributions, these are
generic guidelines to get a working environment:

    * Look for the mandatory requirements in the package manager's repositories of your distribution. Many
      distributions come with ``pip`` package manager which use `PyPI repository <https://pypi.python.org/pypi>`__.
      The required modules are Python (of course), NumPy, SciPy and a BLAS implementation (MKL or OpenBLAS).
      Use the versions recommended at the top of this documentation.
    * If the package manager provide a GCC compiler with the recommended version (see at top), install it. If not,
      you could use the build `TDM GCC <http://tdm-gcc.tdragon.net/>`_ which is provided for both 32- and 64-bit
      platforms. A few caveats to watch for during installation:

          1. Install to a directory without spaces (we have placed it in
             ``C:\SciSoft\TDM-GCC-64``)
          2. If you don't want to clutter your system PATH un-check ``add to
             path`` option.
          3. Enable OpenMP support by checking the option ``openmp support
             option``.
