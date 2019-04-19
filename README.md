# ScientificOSX
These are the steps I took recently to setup a new MacbookPro for scientific/bioinformatics use.

## Step 1, base software:

### 1.1 Install homebrew, update

```{bash }
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew update && brew upgrade
brew config
```
### 1.2 install some basic but nedded libraries:

```{bash }
brew tap brewsci/bio
brew tap brewsci/science
brew tap brewsci/num

brew install tcl-tk
echo 'export PATH="/usr/local/opt/tcl-tk/bin:$PATH"' >> ~/.bash_profile.

brew install libgit2
brew instal fftw
brew install libomp
brew install proj
brew cask install xquartz #may ask for password


brew install Caskroom/cask/mactex
brew install r

```
#### 1.2.2 xml2 package 
For some reason I hit problems installing R packages like kableExtra which require xml2 to be installed.... 

```{bash }
brew install libxml2
R CMD INSTALL --configure-vars='INCLUDE_DIR=/usr/local/opt/libxml2/include/libxml2 LIB_DIR=/usr/local/opt/libxml2/lib/' xml2_1.2.0.tar.gz
```
But if this does not work (didnt for me) as mojave has a different version already installed... 

```{bash }
sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
```

### 1.3 R studio:


Install R studio: https://www.rstudio.com/products/rstudio/download/#download

Using 'brew cask install rstudio' also works but the last time I did that, there was a problem with the version on brew, so just get the latest from above link.

#### 1.3.1 Github setup with Rstudio
To setup SSH keys for easy fast connection between Rstudio and Github: https://happygitwithr.com/ssh-keys.html

#### 1.3.2 Memory issue with Rstudio
At some point I hit an error "ector memory exhausted (limit reached?)"... 

```{bash, }
nano ~/.Renviron

#copy these two lines over then save and quit.
PATH="/usr/local/clang6/bin:${PATH}"

R_MAX_VSIZE=100Gb
```



### 1.4 Docker
```{bash }
brew cask install docker
```

### 1.4 Python and Libs
```{bash }
brew cask install docker

brew install python
brew install python@2

pip install --upgrade distribute
pip install --upgrade pip

pip install Cython

brew install libtiff libjpeg webp little-cms2
pip install Pillow
brew install imagemagick --with-fftw --with-librsvg --with-x11
brew install graphviz --with-librsvg
brew install cairo
brew install py2cairo # this will ask you to download xquartz and install it
brew install qt pyqt5

pip install scipy
pip install numpy

brew install matplotlib --with-cairo --with-tex
pip install pandas
pip install nltk
pip install sympy
pip install q
pip install snakeviz

brew install zmq
pip install ipython[all]
pip install html5lib cssselect pyquery lxml BeautifulSoup
pip install Flask Django tornado
pip install rdflib SPARQLWrapper
pip install networkx

pip install git+git://github.com/scikit-learn/scikit-learn.git
pip install git+git://github.com/statsmodels/statsmodels.git

 pip install umap-learn

```

### 1.4 R and Libs

If you have a current R environment that you use and like, it can help to transfer the libraries to a new computer. 

For convenience, I have the installed_packages.rds stored in /data path. 


```{r }
#in the old computer:

tmp = installed.packages()
installedpackages = as.vector(tmp[is.na(tmp[,"Priority"]), 1])
saveRDS(installedpackages, file="./installed_packages.rds")

#in the new computer:
install.packages("BiocManager")

installedpackages <- readRDS("./installed_packages.rds")
BiocManager::install(installedpackages)

#some packages may not install this way, either they are not on CRAN or Bioconductor or there was a problem. Google each to install. :)


```

#### Specially difficult to install libs

##### Monocle 3 (alpha)

The original source is: https://cole-trapnell-lab.github.io/monocle-release/monocle3/#what-s-new-in-monocle-3

```{r }
source("http://bioconductor.org/biocLite.R")
biocLite()
biocLite("monocle")
devtools::install_github("cole-trapnell-lab/DDRTree", ref="simple-ppt-like")
devtools::install_github("cole-trapnell-lab/L1-graph")

# if everything above is installed, this is not needed as other packages like Seurat also require these
#install.packages("reticulate")
#library(reticulate)
#py_install('umap-learn', pip = T, pip_ignore_installed = T) # Ensure the latest version of UMAP is installed
#py_install("louvain")


devtools::install_github("cole-trapnell-lab/monocle-release", ref="monocle3_alpha")


```

But for this to work, rgdal and sf packages and their dependencies also need to be installed.

From https://www.kyngchaos.com/software/frameworks/  download and install the OSX GDAL framework. I downloaded the 'GDAL_Complete-2.4.dmg'. Also see https://stat.ethz.ch/pipermail/r-sig-mac/2017-June/012429.html if stuck.

The whole point of this is to install https://github.com/r-spatial/sf which depends on gdal and etc.

Install gdal

```{bash }
brew install gdal

```

```{r }
install.packages("sf", configure.args=c('--with-gdal-config=/Library/Frameworks/GDAL.framework/Programs/gdal-config', 
                                        '--with-proj-include=/Library/Frameworks/PROJ.framework/Headers', 
                                        '--with-proj-lib=/Library/Frameworks/PROJ.framework/unix/lib'))

install.packages('rgdal', type = "source", configure.args=c(
  '--with-gdal-config=/Library/Frameworks/GDAL.framework/Programs/gdal-config',
  '--with-proj-include=/Library/Frameworks/PROJ.framework/Headers',
  '--with-proj-lib=/Library/Frameworks/PROJ.framework/unix/lib'))
  
  
```

Now this should run without any errors.
```{r }
devtools::install_github("cole-trapnell-lab/monocle-release", ref="monocle3_alpha")

```

Next, several additional dependencies need to be installed that are tricky also:


For sanity reinstall cairo with brew to the latest. 
```{bash }
brew reinstall cairo
```

Then, add the three lines to nano ~/.R/Makevars below and save close and restart R.

```{bash }
CAIRO_CFLAGS = /usr/local/include
CAIRO_LIBS = /usr/local/opt/cairo
PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
```
now installing Cairo in R should work, followed by ggraster.

```{r }
install.packages("Cairo")

devtools::install_github('VPetukhov/ggrastr')

```






## Step 2, Useful Apps:

1. Atom to edit anything. From txt to markdown. https://atom.io/
2. Box sync. Setup as directed. https://ohsu.account.box.com/login
3. Evernote. https://evernote.com/
4. Mendeley. https://www.mendeley.com/
5. Latex Editor, TexStudio. https://www.texstudio.org/
6. VLC: https://www.videolan.org/vlc/download-macosx.html
7. Mozilla Firefox: https://www.mozilla.org




## Step 3, Extra features, personal.

Halfstar Itunes:
defaults write com.apple.iTunes allow-half-stars -bool TRUE
