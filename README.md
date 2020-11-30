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
    putup python-package
    mv python-package/* .
    rm -rf python-package
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
    │   └── example_project                   <- the package code 
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
- optional: under build_sphinx -> change the build dir build_dir = build/sphinx to build_dir = docs/_build

# Create development environment
    python setup.py develop