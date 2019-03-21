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
brew install libxml2
brew cask install xquartz #may ask for password


brew install Caskroom/cask/mactex
brew install r

```
### 1.3 R studio:


Install R studio: https://www.rstudio.com/products/rstudio/download/#download

Using 'brew cask install rstudio' also works but the last time I did that, there was a problem with the version on brew, so just get the latest from above link.

#### 1.3.1 Github setup with Rstudio
To setup SSH keys for easy fast connection between Rstudio and Github: https://happygitwithr.com/ssh-keys.html

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
