# Conda

## Environments
Conda makes it easy to manage multiple different environments (particular software at particular versions) on your computer. This allows you to easily switch between environments, create new environments, and share environments with others (or your future self). 

As an example of where this is useful, I recently had a minor crisis when I went to run some code and it tripped a bunch of errors with no clear fix. I hadn't touched it since I ran it without issue a month ago, but suddenly there were all these errors. Some digging showed that a python library had been upgraded in the meantime, creating the issue. I was able to make a new environment with the old library version, and re-run without issue. Now, I try to save an `environment.yml` with every project. 

Other great resources about environments:
- [Conda Cheat Sheet](https://conda.io/docs/_downloads/conda-cheatsheet.pdf)
- Conda Documentation: [Managing environments](https://conda.io/docs/user-guide/tasks/manage-environments.html)
- [My Python Environment Workflow with Conda](https://tdhopper.com/blog/my-python-environment-workflow-with-conda/) by Tim Hopper

## General
### List envs
`conda info --envs`

OR

`conda env list`

### Activate environment 
`source activate myenv`

### Remove environment
`conda remove --name myenv --all`

## History
You can see the history by running:

`conda list --revisions`

...and update to a previous revision by running:

`conda install --revision 1`

See more [here](http://blog.rtwilson.com/conda-revisions-letting-you-rollback-to-a-previous-version-of-your-environment/)


## txt
### Create environment from `env.txt`
`conda env create --file env.txt`

or 

`conda create --name <env> --file <this file>`

### Save current environment to `env.txt`
`conda list --explicit > env.txt`

## yml
### Create environment from `environment.yml`
`conda env create -f environment.yml`

Note: the environment name is defined in the `environment.yml` so no need to specify

### Save current environment to `environment.yml`
`conda env export > environment.yml`

