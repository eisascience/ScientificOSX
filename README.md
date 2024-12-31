# ScientificOSX

These are the steps I took recently to setup a new MacbookPro (Sonoma OS 14.7.2) for scientific/bioinformatics use.

## Step 1, base software:

Log in to App Store with login. Xcode and other needed items are autodownloaded by homebrew via the App Store.

Start Xcode & accept terms.

### Install homebrew, update

```{bash }
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

brew analytics off

brew update && brew upgrade

brew config

```

### Extras

```{bash }
#skip this, its pedantic

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
alias rc="source ~/.bash_profile"

#alias man="_() { echo $1; man -M $(brew --prefix)/opt/coreutils/libexec/gnuman $1 1>/dev/null 2>&1;  if [ "$?" -eq 0 ]; then man -M $(brew --prefix)/opt/coreutils/libexec/gnuman $1; else man $1; fi }; _"

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

### R and R studio:

install https://rud.is/rswitch/
Install latest R: https://cran.r-project.org/bin/macosx/
RStudio: https://www.rstudio.com/products/rstudio/download/#download

At this time, I need 4.2 and 4.4 so I installed them both respectively. 

#### Multiple versions of R

Blindly using the binary installer (*.pkg) version available through CRAN will remove the current version of the r framework (including your package libraries). 

Thus, prior to installing the new version of R is trick OSX into forgetting that R is already installed on your system by using rswitch.

https://rud.is/rswitch/guide/index.html



```{bash}
#this is old stuff hoarding just in case

pkgutil --pkgs #shows what is installed
#updated for catalina, and I installed 4.0 first then 3.6 and the below code worked great.
#Make sure you copy over the RSwitch.App to your applications folder and run it.

sudo pkgutil --forget org.R-project.R.fw.pkg
sudo pkgutil --forget org.r-project.x86_64.tcltk
sudo pkgutil --forget org.R-project.R.GUI.pkg
             
             
```

### Base Needs

```{bash}
brew install hdf5 git freetype
brew install cmake automake fontconfig jpeg libtiff libpng libffi doxygen
brew install glib libcaca libconfig libtasn1 libtool libunistring zlib icu4c
brew install tmux
```

### Python and Libs

#### management of different python versions

There are a number of tools available that enable the installation and management of different python versions.

pyenv is one tool to do this. One could also use anaconda or miniconda or similar. 

```{bash }
#skip for now, later we can use a flavor of conda
brew install pyenv
echo "eval "$(pyenv init -)"" >> ~/.bash_profile
source ~/.bash_profile
pyenv install --list

#see list for latest
#pyenv install 3.9.1 # 3.9 does not support Numpy
pyenv install  3.8.7
pyenv install 2.7.18

#set globally which python
pyenv global 3.8.7
pyenv version

#update pip
pip install --upgrade pip

```
#### virtual python environments 

To have different python projects with different dependencies and versions of python; environments help isolate them.

to create python virtual environments using pipenv:

```{bash }
#skip for now, later we can use a flavor of conda

brew install pipenv


mkdir MyPyTest
cd MyPyTest
pipenv --python 3.8

#to install packages use pipenv within the environment

pipenv install ipykernel


```
Note: Jupyter Notebooks are able to work with virtual environments so that you are able to run the notebooks for a project in the correct project environment.

```{bash}
#skip for now, later we can use a flavor of conda

#change myenv to a name
python3 -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

#### Python Packages

jupyter notebook can be invoked which will automatically open a window in your browser.


```{bash }
pip3 install notebook
pip3 install h5py
pip3 install umap-learn

```



### Extra installs

```{bash }
#skip for now
Install latest gfortran https://github.com/fxcoudert/gfortran-for-macOS/releases

```

### R packages 

Note if you have multiple R environments, you may want to do this for each.

```{bash}
#update Rprofile by adding the line below and saving
nano ~/.Rprofile.site
# local({options(repos = BiocManager::repositories())})

```



```{r}

install.packages(c("devtools", "BiocManager", "remotes"), dependencies=TRUE, ask = FALSE)

BiocManager::install(c("BiocParallel", "DropletUtils", "ExperimentHub", "SingleCellExperiment"), dependencies=TRUE)
BiocManager::install(c("SingleR", "celldex", "DESeq2", "MAST", "scDblFinder", "ComplexHeatmap", "clusterProfiler", "RUVSeq", "escape", "GSVA", "decoupleR", "OmnipathR", "monocle", "princurve", "vegan", "RSelenium", "wordcloud" , "ggpubr"), dependencies=TRUE)
BiocManager::install(c("org.Hs.eg.db", "org.Mm.eg.db", "HSMMSingleCell", "DelayedMatrixStats", "DESeq2", "genefilter", "preprocessCore", "demuxmix"), dependencies=TRUE)
BiocManager::install(c("preprocessCore", "demuxmix"), dependencies=TRUE)

devtools::install_github("karthik/wesanderson")
devtools::install_github("marchinilab/SDAtools")
devtools::install_github("davidsjoberg/ggsankey")
devtools::install_github("VPetukhov/ggrastr")
remotes::install_github("juba/rmdformats")

devtools::install_github(repo = "bimberlabinternal/cellmembrane", dependencies = TRUE)
devtools::install_github(repo = "eisascience/scCustFx", dependencies = TRUE)
devtools::install_github(repo = "bimberlab/cellhashR", ref = "master", dependencies = TRUE)
devtools::install_github(repo = "bimberlabinternal/Rdiscvr", dependencies = TRUE)
devtools::install_github(repo = "bimberlabinternal/rira", dependencies = TRUE)

# install.packages("XML", repos = "http://www.omegahat.net/R")





```

### cask software

```{bash]
brew install --cask cyberduck
brew install --cask docker



```



