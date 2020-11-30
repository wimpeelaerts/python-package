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

