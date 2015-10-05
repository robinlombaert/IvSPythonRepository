* Clone the git repository to create a local copy in an "ivs" folder. 
  
    $ cd python/
    $ git clone https://github.com/robinlombaert/IvSPythonRepository.git ivs

  This will clone all repository files in the ~/python/ivs folder. Be aware, however, that only the python scripts and the documentation are being cloned, not the (numerous and sometimes huge) datafiles that come along with it, containing, for example, limbdarkening coefficients.
    
* Updating your own clone of the IvS python repository to the most recent version can be done with

    $ cd ivs
    $ git pull

* Make sure that your python path points to the ivs folder, so that you can simply import
using, for example:

    >>> from ivs.statistics import linearregression

  If your python repository is in, e.g., ~/python/ivs/ , you can put in your .bash_profile:
  
    export PYTHONPATH=/home/YOURNAME/python:$PYTHONPATH

  Warning: don't put ~/python/ivs in your Python path, but just ~/python.

* For the next part of the installation, temporarily move the io folder elsewhere, e.g.

    $ cd ivs
    $ mv io io_backup

* In the config.py file in the ivs folder, add the path where the IvS data catalogs (variable: data_dir) can be found. 

* The IvS Python repository contains mostly python routines. Some of the time-critical
functions, however, are written in fortran. This assumes you have gfortran installed on your system. To compile them you can run

    $ python config.py compile

Alternatively, if you want to specify your own fortran compiler you can do so with

    $ python config.py compile f77

Note: sometimes the compilation process fails. If so, try to compile spectra/pyrotin4.f manually, and then retry the automatic compilation:
    
    $ cd spectra/
    $ f2py --fcompiler=gfortran -c pyrotin4.f -m pyrotin4
    $ cd ../
    $ python config.py compile

* With the installation finished, move the io folder back:

    $ cd ivs
    $ mv io_backup io

* To generate the documentation (which, as a user, you typically do not have to do), simply run the script

    $ python makedoc.py

  in the repository's root folder. This assumes that 'epydoc' is available which is 
  already installed on all IvS computers. On your own laptop, you can get it from 
  http://epydoc.sourceforge.net.
 
Open "/doc/html/index.html" in your favorite browser and start browsing!
Whenever you change something yourself in your local branch or you pull changes
from someone else, you can re-run the makedoc.py script.

  
* Happy computing!





Encountered errors and their solutions:
=======================================

1. Q: When I run "python config.py compile", I get the following error: 
numpy.distutils.fcompiler.CompilerNotFound: gnu95: f90 nor f77
A: Install gfortran.

2. Q: When I run "python config.py compile", I get the following error: 
/bin/sh: f2py: command not found
A: Install f2py. If you do have f2py installed, but under a different name for the executable (for instance, f2py-2.7), replace f2py with f2py-2.7 in config.py (search for cmd = ).
