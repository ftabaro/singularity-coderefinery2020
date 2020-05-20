# JupyterLab container for CodeRefinery 2020

This repository contains the recipe for the container used in CodeRefinery Workshop 2020 by the NykterLab team.

## What's inside
- The base container is Jupyter datascience-notebook Docker container. 
- Few Python packages have been added, e.g.: 
   - `sphinx`
   - `pytest` 
   - `pycodestyle`
- Two Jupyter extensions:
   - JupyterLab Git
   - JupyterLab GitHub

## Build

1. Clone this repository
2. Build
```
sudo singularity build coderefinery.sif Singularity
```

## Run

```
singularity exec -B /run/user coderefinery.sif jupyter lab [options]
```

All JupyterLab options are supported by the command above.

## Configure the GitHub integration

In order to use the GitHub integration, an authentication token needs to be generated from GitHub and Jupyter lab needs to be configured to use it.

To generate a token:
1. Navigate to profile settings on GitHub: https://github.com/settings/profile
2. On the menu on the left, click "Developer Settings"
3. On the menu on the left, click "Personal Access Tokens"
4. Click on top right button "Generate new token" 
5. In the "Note" field insert a suitable name, e.g. "Jupyter"
6. In the "Select scopes" menu, click on "repo" to allow full control of private repositories
7. At the bottom of the page, click on "Generate token" 
8. At this point take note of the code in the green box, copy it and paste it to some secure place

To configure Jupyter to use the token:
1. Connect to the machine running the Jupyter container instance (e.g. narvi)
2. If the file `~/.jupyter/jupyter_notebook_config.py` exists, skip the next step
3. Generate a config file with:
```
singularity exec containers/coderefinery.sif jupyter notebook --generate-config
```
4. Open the `~/.jupyter/jupyter_notebook_config.py` file with a text editor
5. Navigate to the bottom of the file and add the following line replacing `< YOUR_ACCESS_TOKEN >` with the token generated above
```
c.GitHubConfig.access_token = '< YOUR_ACCESS_TOKEN >'
```


At this point, starting the JupyterLab instance, no error message will be displayed and the user will be able to navigate GitHub repositories from the JupyterLab UI.

## References

- [Online CodeRefinery workshop](https://coderefinery.github.io/2020-05-25-online/)
- [Singularity](https://sylabs.io/guides/3.3/user-guide/quick_start.html)
- [Jupyter datascience-notebook Docker image](https://hub.docker.com/r/jupyter/datascience-notebook)
- [GitHub token creation](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)
- [JupyterLab Git extension](https://github.com/jupyterlab/jupyterlab-git)
- [JupyterLab GitHub extension](https://github.com/jupyterlab/jupyterlab-github)


