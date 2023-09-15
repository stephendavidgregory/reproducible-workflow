---
title: "README"
---

This repo holds the files that I use for my attempted reproducible workflow.

This is the Win MS dos script, called something like `new-git-project.cmd`, to set up a new project, where `[YOUR PATH]` (e.g., "C:\Users\You\git\reproducible-workflow") is the directory to the "template-manuscript-git-v1.*" files (i.e., this cloned repo?):

```

:: create a new git project

:: keep silent
@echo off

:: your path without the trailing "\"
set yp="[YOUR PATH]"

:: get project name
set /P pnm="Please enter project name... "

:: make directory structure - see https://drivendata.github.io/cookiecutter-data-science/
mkdir %pnm%
cd %pnm%
mkdir data
mkdir plots
mkdir results
mkdir scripts


:: COPY FILES

:: copy over and rename .Rmd ms template
cp.exe %yp%\template-manuscript-git-v1.qmd .\%pnm%.qmd

:: copy over and rename .R script templates
cp.exe %yp%\template-manuscript-git-v1-rsetup.R .\scripts\r-setup.R
cp.exe %yp%\template-manuscript-git-v1-libsfuns.R .\scripts\libraries-and-functions.R
cp.exe %yp%\template-manuscript-git-v1-anlyopts.R .\scripts\analysis-options.R
cp.exe %yp%\template-manuscript-git-v1-globvars.R .\scripts\global-variables.R
cp.exe %yp%\template-manuscript-git-v1-close.R .\scripts\close.R
cp.exe %yp%\template-manuscript-git-v1-orgdata.R .\scripts\00-orgdata.R
cp.exe %yp%\template-manuscript-git-v1-analysis1.R .\scripts\01-analysis1.R

:: copy over and rename .Rproj file
cp.exe %yp%\template-manuscript-v1.Rproj .\%pnm%.Rproj

:: copy over biblio stuff
cp.exe %yp%\ecology.csl .\ecology.csl
cp.exe %yp%\references.bib .\references.bib

:: make an empty readme
echo. | set /p=>README.md

:: make an empty readme
echo. | set /p=>TODO.md


:: FIXES

:: replace __PATH__ with path
:: echo %cd% | sed "s/\\\/\\//g" > foo.txt
:: sed -i 's/ $/\//g' foo.txt
:: set /p dnm=<foo.txt
:: set dnm="\"%dnm%\""
:: rm.exe foo.txt
:: powershell -Command "(gc .\%pnm%.Rmd) -replace '__PATH__', '%dnm%' | sc .\%pnm%.Rmd"


:: initialise GIT
git init

:: copy over gitignore
cp.exe %yp%\.gitignore .\.gitignore

:: message
pause

```

You'll notice that the `:: FIXES` are commented out - I'm not sure how useful it is...


## To do...

1.   Generalise plot making and saving by using:

```
## get plot objects
p_objs <- ls(pattern = "_p$")
```

rather than (for example):

```
## get plot objects
p_objs <- c("ew_adult_returns_p")
```

and then plotting can be a separate script...?


2.   Delete all but some files at the beginning of each script so that when they are run together, then objects don't accumulate during the saves...


3.   Fix changelogs
