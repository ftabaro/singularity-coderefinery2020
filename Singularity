Bootstrap: docker
From: jupyter/datascience-notebook:latest

%help
  Extended jupyter/datascience-notebook with packages for CodeRefinery workshop

%labels
  Author francesco.tabaro@tuni.fi
  Version 0.1

%post
  PATH=/opt/conda/bin:$PATH && \
  conda install --quiet --yes sphinx sphinx_rtd_theme pytest pycodestyle && \
  conda install --quiet --yes -c conda-forge jupyterlab-git nbdime ipywidgets && \
  conda clean --all -f && \
  pip install jupyterlab_github && \
  jupyter lab build && \
  jupyter labextension install @jupyterlab/github

%environment
  export PATH=/opt/conda/bin:$PATH
  
