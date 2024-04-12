# Howto use Juypter

## Login
Go to : https://jupyter.analyticsinternal.iunera.com 
Log in with azure ad

## Choose a Profile
* iunera Datascience environment


# How to use git

## Configure credential helper
Open a Terminal in your Juypter Notebook `File->new->Terminal`

Add the following command line
```
git config --global credential.helper store
```

# Customize Images
You might need some additional Libs installed. You can just do this inside your environment (`File->new->Terminal`) using pip or conda.
If you want to change the notebook images here e.g. the `datascience-notebook` create a branch and extend the `Dockerfile`. The Juypterhub entry `iunera Datascience environment LATEST-DEV IMAGE` always pulls the lastet image build from a branch. 
If you are done send a Pull Request to Tim or me. 
The new Stable Image needs to be applied in the Juypter Helmchart (can only be done by me or Tim.)