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
export PATH=/usr/local/sbin:$PATH
export PATH="$(brew --prefix coreutils)/libexec/gnubin:$PATH"
alias edit='open -a /Applications/TextEdit.app/'
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


### Python and Libs

```{bash }
brew install python


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



