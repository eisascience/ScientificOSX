# ScientificOSX
These are the steps I took recently to setup a new MacbookPro for scientific/bioinformatics use.

## Step 1, base software:

### Install homebrew, update

```{bash }
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

brew analytics off

brew update && brew upgrade

brew config

```

### JAVA

```{bash }
brew tap AdoptOpenJDK/openjdk
brew cask install adoptopenjdk11

```

### R studio:

Install latest R & R studio: https://www.rstudio.com/products/rstudio/download/#download


### Python and Libs
```{bash }

brew cask install xquartz

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

```



