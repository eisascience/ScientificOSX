# ScientificOSX
These are the steps I took recently to setup a new MacbookPro for scientific/bioinformatics use.

## Step 1, base software:

### 1.1 Install homebrew, update

```{bash }
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

brew analytics off

brew update && brew upgrade

brew config

```

### 1.2 R studio:

Install latest R & R studio: https://www.rstudio.com/products/rstudio/download/#download


### 1.4 Python and Libs
```{bash }

brew cask install xquartz

brew install python


pip3 install umap-learn

```


