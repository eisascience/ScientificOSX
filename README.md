# ScientificOSX

These are the steps I took recently to setup a new MacbookPro (Catalina OSX 10.15.7) for scientific/bioinformatics use.

## Step 1, base software:

Log in to App Store with login. Xcode and other needed items are autodownloaded by homebrew via the App Store.


### Install homebrew, update

```{bash }
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

brew analytics off

brew update && brew upgrade

brew config

```

### Extras

```{bash }
#update bash
bash --version

brew install bash

#The newer version of bash is located at /usr/local/bin/bash:
ls -l /usr/local/bin/bash
cat /etc/shells


# If not in /etc/shells, append it:
sudo -i
echo /usr/local/bin/bash >> /etc/shells

#Set default shell to /usr/local/bin/bash, run the following chsh command
chsh -s /usr/local/bin/bash

#should have changed to latests
bash --version

```

### Create 

```{bash }
touch ~/.bash_profile
# to edit use nano 
nano ~/.bash_profile



```
Include this in ~/.bash_profile & save. 

```{bash }
export PATH=/usr/local/bin:/usr/local/sbin:$PATH
alias rc='source ~/.bash_profile'
alias man='_() { echo $1; man -M $(brew --prefix)/opt/coreutils/libexec/gnuman $1 1>/dev/null 2>&1;  if [ "$?" -eq 0 ]; then man -M $(brew --prefix)/opt/coreutils/libexec/gnuman $1; else man $1; fi }; _'

```

```{bash }
source ~/.bash_profile
```

### Xquartz

```{bash }

brew install --cask xquartz

```

### JAVA

```{bash }
brew tap AdoptOpenJDK/openjdk
brew install --cask adoptopenjdk11

```

### R studio:

Install latest R & R studio: https://www.rstudio.com/products/rstudio/download/#download

### Base Needs

```{bash}
brew install hdf5

```

### Python and Libs

#### management of different python versions

There are a number of tools available that enable the installation and management of different python versions.

pyenv is one tool to do this.

```{bash }
brew install pyenv
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
source ~/.bash_profile
pyenv install --list

#see list for latest
#pyenv install 3.9.1 # 3.9 does not support Numpy
pyenv install  3.8.7
pyenv install 2.7.18
```
#### virtual python environments 

To have different python projects with different dependencies and versions of python; environments help isolate them.

to create python virtual environments using pipenv:

```{bash }
brew install pipenv


mkdir MyPyTest
cd MyPyTest
pipenv --python 3.8

#to install packages use pipenv within the environment

pipenv install ipykernel


```
Note: Jupyter Notebooks are able to work with virtual environments so that you are able to run the notebooks for a project in the correct project environment.

```{bash}
#change myenv to a name
python3 -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

#### Python Packages

jupyter notebook can be invoked which will automatically open a window in your browser.


```{bash }
pip3 install notebook

pip3 install umap-learn

```



### Extra installs

```{bash }

Install latest gfortran https://github.com/fxcoudert/gfortran-for-macOS/releases

```

### R packages 

```{r}

install.packages(c('devtools', 'BiocManager', 'remotes'), dependencies=TRUE, ask = FALSE)

options(repos = BiocManager::repositories())

BiocManager::install(c('org.Hs.eg.db', 'org.Mm.eg.db', 'HSMMSingleCell', 'monocle', 'DelayedMatrixStats', 'DESeq2', 'genefilter'), dependencies=TRUE, ask = FALSE)

#installs Seurat as part of the OOSAP package and dependencies
devtools::install_github(repo = 'bimberlabinternal/OOSAP', ref = 'Dev', dependencies = T, upgrade = 'always')

devtools::install_github('VPetukhov/ggrastr')

```

### cask software

```{bash]
brew cask install cyberduck
brew cask install mendeley
brew cask install TexStudio
brew cask install docker

```



