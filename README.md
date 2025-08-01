# Lecture Template
This repo contains a template for lecture materials prepared with Quarto. 


```
git clone git@github.com:thomasmanke/website_qmd.git
m website_qmd
micromamba create -n <project_name> website_qmd/micromamba.yml -y
micromamba activate <project_name>


quarto use template thomasmanke/website_qmd
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