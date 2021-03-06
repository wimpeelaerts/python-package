# python-package
skeleton for a python package

# Setup 
Create GIT repo and create master en develop branch 

    git clone https://github.com/wimpeelaerts/python-package.git
    cd python-package
    git config --global user.name wimpeelaerts
    git checkout -b master
    git push origin master
    git checkout -b develop
    git push origin develop
    git branch -d main
    git push origin --delete main


# Skeleton with PyScaffold 
Use the default command to create the blueprint of the package

    conda install -c conda-forge pyscaffold
    putup python_package
    mv python_package/* .
    mv python_package/.* .
    rm -rf python_package
    rm requirements.txt

# Create condaenvironment
Do this to isolate the dependancies for the development of this package 

    conda create -n python-package python=3
    conda activate python-package

# Folder layout

    ├── AUTHORS.rst                
    ├── CHANGELOG.rst
    ├── LICENSE.txt
    ├── README.rst
    ├── docs                                <- package documentation (Sphinx)
    │   ├── Makefile
    │   ├── _static
    │   ├── authors.rst
    │   ├── changelog.rst
    │   ├── conf.py
    │   ├── index.rst
    │   └── license.rst
    ├── requirements.txt                    <- delete this file, requirements defined in setup.cfg
    ├── setup.cfg                           <- MAIN CONFIGURATION FILE!
    ├── setup.py                            <- leave untouched, config is defined in setup.cfg
    ├── src                                
    │   └── python_package                  <- the package code 
    │       ├── __init__.py
    │       └── skeleton.py
    └── tests                               <- unit tests (pytest)
        ├── conftest.py
        └── test_skeleton.py

# Update setup.cfg 

- optional: fill in metadata
- smart thing to do: uncomment "install_requires" and add packages dependancies here
- smart thing to do: add a develop section under options.extras_require and add development dependancies here

        develop =
            pytest
            pytest-cov
            sphinx
            sphinx_rtd_theme  # optional if you want to use rtd theme
            pre-commit
            black

- smart thing to do: under tool:pytest -> replace "term-missing" with "html"  (report documentation as html)

# Create development environment

Install the package dependancies ("install_requires" in setup.cfg). This will create and simlink the python_package.egg in your conda env

    python setup.py develop

Install the test and develop dependancies (You would think "tests_require", but no, this field is not strictly enforced by setuptools)
PyScaffold’s recommendation is to use a filed in the "options.extras_require" section like we did (develop). then 

    pip install -e .[develop]

# First use 

Use the module "skeleton" in your package "python_package" to call the fib() function in a Python session. 

    python
    import python_package as pp
    pp.skeleton.fib(10)

    import python_package.skeleton as skeleton
    skeleton.fib(10)

Do the same from te commandline 

Add a following lines to the section "options.entry_points" in setup.cfg. This will create the function run in the skeleton module as an enterypoint for the fibonacci cmd. 

    console_scripts =
        fibonacci = python_package.skeleton:run

bash:

    python setup.py develop
    fibonacci 10 

# Unit tests (pytest)

More info on unit tests [pytest.org](https://docs.pytest.org/en/latest/). All files starting with "test_" in the folder tests is picked up and executed. 

    Unit tests (pytest)

# Sphinx Documentation

    python setup.py docs

## Optional: Get the read the docs look and feel 

Change the docs/conf.py file 

- add "import sphinx_rtd_theme" statement on top
- adjust the html_theme to html_theme = 'sphinx_rtd_theme'
- uncomment/adjust html_theme_path to html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
- drop the html_theme_options

check docs\_build\html folder for the result

## Module reference

Automatic creation of the API classes/modules documentation when code is propper documented using [numpydoc](https://numpydoc.readthedocs.io/en/latest/format.html) format 

# Optional Code formatting

Enforce PEP8 style guide via pre-commit 
Check ".pre-commit-config.yaml" in the package root folder 

    pre-commit install

# Create distribution

- Source distribution(sdist): includes readeble py files 

        python setup.py sdist

- Built distribution(bdist): includes compiled pyc files -> specific to a platform and Python version.

        python setup.py bdist
        python setup.py bdist_wheel

# Distibute distributions 

## PIP
Build the package (python setup.py sdist, python setup.py bdist, python setup.py bdist_wheel) on a share filesystem (e.g. /home/wimpeelaerts/python-package/dist)

    conda deactivate 
    conda create -n test python=3
    pip install /mnt/c/Users/peelaerw/python-package/dist/python_package-1.0.0.tar.gz    

## Conda

    setup.py bdist_conda

!Better to use conda-build! ToDo


# Hookup with CI/CD