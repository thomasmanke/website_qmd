# Lecture Template
This repo contains a template for lecture materials prepared with Quarto. 

## Option 1 (clone as usual):
```
# clone as usual
git clone git@github.com:thomasmanke/website_qmd.git
```

## Option2 (if quarto is already installed)
```
mkdir project_name
cd project_name

# create a new quarto project
quarto use template thomasmanke/website_qmd

# preview the website
quarto preview
```

## Setup
In any case you might want to create a minimal environment to include python, quarto and a few very common packages.

Notice that this is not the same environment as used by most lectures that have their own environment files. 

```
micromamba create -n <project_name> website_qmd/micromamba.yml -y
micromamba activate <project_name>
```





# Initial Commit

```
git init
git add .
git commit -m "Start template for website development with quarto" 

# Create a new repository on GitHub: thomasmanke/website_qmd.git

git remote add origin git@github.com:thomasmanke/website_qmd.git
git push -u origin main
```