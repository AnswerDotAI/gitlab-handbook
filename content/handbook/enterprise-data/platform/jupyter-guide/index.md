---
title: "Jupyter Guide"
description: "Guidance on setting up JupyterLab"
---

---
See related [repository](https://gitlab.com/gitlab-data/data-science)

## Features

- Virtual environment install of JupyterLab with the most useful extensions pre-installed
- Common python DS/ML libraries (pandas, scikit-learn, sci-py, etc.)
- Natively connected to Snowflake using your dbt credentials. No login required!
- Git functionality: push and pull to Git repos natively within JupyterLab ([requires ssh credentials](https://docs.gitlab.com/ee/user/ssh.html))
- Run any python file or notebook either from your local machine or in a GitLab repo
- Support for running Jupyter in VS Code
- Need a feature you use but don't see? Let us know on [#bt-data-science](https://gitlab.slack.com/archives/C027285JQ4E)

## Getting Started

JupyterLab is configured to run in a [virtual environment](https://docs.python.org/3/library/venv.html) on your local machine. If you prefer not to setup a virtual environment, you can instead use the [data science docker image](https://gitlab.com/gitlab-data/data-science/container_registry/6712928) with CUDA support.

When setting up JupyterLab, the following will happen:

- [uv](https://astral.sh/blog/uv) will create and manage a Python virtual environment in `.venv/` containing all required packages. uv is extremely fast and a great replacement tool for many common python tools (pipenv, pip-compile, install, etc.)
- A virtual python environment will be created using uv and the python version and packages (and their dependencies) defined in [pyproject.toml](https://gitlab.com/gitlab-data/data-science/-/blob/main/pyproject.toml)
- JupyterLab will be built within the venv

## Installation Instructions

**Note:** This setup is geared towards MacOS. The code may also work on Linux or Windows with some modifications. 

1. Prerequisites - before installing please make sure the following are installed on your local machine:
   - [Python3.11+](https://www.python.org/)
   - [Pip3](https://pypi.org/project/pip/) (usually aliased as `pip`).
   - [Git](https://git-scm.com/downloads/mac)
   - Certain versions of MacOS may require Xcode Command Line Tools to be installed. From the command line, `xcode-select --install`
1. Clone the data-science repo to your local machine `git clone git@gitlab.com:gitlab-data/data-science.git`
1. Navigate to the directory: `cd data-science`
1. Execute the following command: `make setup`. This will do several things:
   - Check, and if necessary, install/update brew, node.js, uv, and certain python packages on your local machine. 
   - Setup a virtual environment in the `data-science` directory
1. Launch Jupyter
   - To launch JupyterLab: `make jupyter`
   - To launch VS Code with a Jupyter Server: `make jupyter-vscode` then follow the terminal instructions

### Running from Docker

Although we recommend running JupyterLab from a virtual environment, sometimes that is not always possible. In those instances, we have created a docker image that can be used.

1. Pull the image `registry.gitlab.com/gitlab-data/data-science/datascienceimage:latest` into your container manager (we prefer [Rancher Desktop](https://rancherdesktop.io/))
1. Use the [docker-compose.yml](https://gitlab.com/gitlab-data/data-science/-/blob/main/docker-compose.yml) to launch JupyterLab. In your terminal, navigate to the location of the data-science repository on your local machine and type `make jupyter-docker`
1. You will need to manually copy and paste the URL shown in the terminal into your web browser to load JupyterLab

### Mounting a local directory

By default, the local install will use the `data-science` folder as the root directory for JupyterLab. This is not terribly useful when your code, data, and notebooks are in other locations on your computer. To change, this you will need to create and modify a Jupyter Notebook config file:

1. Open terminal and navigate to the data-science repo, e.g. `cd repos/data-science`. 
1. Run `./.venv/bin/jupyter lab --generate-config` which generates `/Users/{your_user_name}/.jupyter/jupyter_lab_config.py`.
1. Browse to the file location and open it in a text editor
1. Search for the following line in the file: `#c.ServerApp.root_dir = ''` and replace with `c.ServerApp.root_dir = '/the/path/to/other/folder/'`. If unsure, set the value to your repo directory (i.e. `c.ServerApp.root_dir = '/Users/{your_user_name}/repos'`). Make sure you remove the `#` at the beginning of the line.
1. Make sure you use forward slashes in your path. Backslashes could be used if placed in double quotes, even if folder name contains spaces as such as `\{your_user_name}\Any Folder\More Folders\`
1. Rerun `make jupyter` from the data-science directory and your root directory should now be changed to what you specified above.

### Enabling Jupyter Templates

The data science team has created modeling templates that allow you to easily start building predictive models without writing python code from scratch. To enable these templates:

- In your `jupyter_lab_config.py` that you created as part of the [Mounting a local directory](/handbook/enterprise-data/platform/jupyter-guide/#mounting-a-local-directory), add the following lines, replacing `/Users/{your_user_name}/repos/` with the path to the `data-science/templates` repo on your local machine:

```py
c.JupyterLabTemplates.template_dirs = ['/Users/{your_user_name}/repos/data-science/templates']
c.JupyterLabTemplates.include_default = False
```

- Launch JupyterLab and you should see a new *Template* icon. Click the icon and select which template you would like to use.
![alt text](/images/enterprise-data/platform/jupyter-guide/jupyter-screen-shot.png)

### Setting Up Jupyter Extensions

- The data-science repo comes with many useful JupyterLab extensions pre-installed, including [git](https://github.com/jupyterlab/jupyterlab-git) and [execute time](https://github.com/deshaw/jupyterlab-execute-time), and [system monitor](https://github.com/jtpio/jupyterlab-system-monitor).
- To get the most out of these (and to avoid having to configure them every time you run the container), create the following file: `/Users/{your_user_name}/.jupyter/lab/user-settings/@jupyterlab/notebook-extension/tracker.jupyterlab-settings`
- Within that file, paste the following and save:

```json
{
    "codeCellConfig": {
        "codeFolding": true,
        "lineNumbers": true,
    },

    "recordTiming": true,

}
```

### Updating the Virtual Environment

1. From the data-science repo, pull the latest changes to your local machine `git pull`
1. ***Optional:*** You may update the dependencies using the `make recompile` command, or add/remove dependencies using `make add-packages` and `make remove-packages`
1. Re-run `make setup`
1. Launch JupyterLab via `make jupyter` or `make jupyter-vscode`

## Connecting to Snowflake

1. Make sure on your local machine you have setup `/Users/{your_user_name}/.dbt/profiles.yml` file which **does not** include your password. `profiles.yml` must be placed in this directory in your "home" directory otherwise you will not be able to connect to Snowflake from your local machine. You can use the [sample profile](https://gitlab.com/gitlab-data/analytics/-/blob/master/admin/sample_profiles.yml) as a reference
1. Run through the [auth_example notebook](https://gitlab.com/gitlab-data/data-science/-/blob/main/examples/auth_example.ipynb) in the repo to confirm that you have configured everything successfully. You will get a browser redirect to authenticate your Snowflake credentials through Okta.
1. If you get an error then likely Snowflake is not properly configured on your machine. Please refer to the Snowflake and dbt sections of the [Data Onboarding Issue](https://gitlab.com/gitlab-data/analytics/-/blob/master/.gitlab/issue_templates/Team%3A%20Data%20Onboarding.md). It is likely that your .dbt/profiles.yml is not setup correctly.

## Connecting to GitLab Model Experiments (MLFlow Integration)

1. In your GitLab profile, create a personal access token access token with API permissions
1. Ensure that **Model experiments** is toggled on under **Settings -> General -> Visibility, project features, permissions** for your project in GitLab
1. Locate the project id for your project under **Settings -> General**
1. On your local machine, you will need to create two new environment variables `MLFLOW_TRACKING_TOKEN` and `MLFLOW_TRACKING_URI`
   1. Open up your shell resource file (`.zshrc`, for example) in your local machine home directory.
   1. Add the following line `export MLFLOW_TRACKING_TOKEN="your-access-token"`
   1. Add the following line `export MLFLOW_TRACKING_URI="https://gitlab.com/api/v4/projects/{your-project-id}/ml/mlflow"`, but with your project id. Alternatively, you can also place this directly in your notebook.
   1. Save the file
   1. Source the file (i.e. `source ./zshrc`) or exit terminal and restart
1. Launch JupyterLab. You should now be able to initialize the experiment tracker with the `mlflow.set_tracking_uri(os.getenv('MLFLOW_TRACKING_URI'))`command in JupyterLab

**Note:** If looking to connect to the Model Experiments when using CI, refer to [Model Training Step-by-Step Instructions](/handbook/enterprise-data/platform/ci-for-ds-pipelines#model-training-step-by-step-instructions)

## Some interesting libraries included

### Data & Model Management

- [GitLabDS](https://pypi.org/project/gitlabds/): Tools to quickly perform common EDA tasks
- [MLFlow](https://mlflow.org/docs/latest/index.html): Experiment tracking and model registry
- [Feast](https://feast.dev/): Open-source feature store
- [Papermill](https://papermill.readthedocs.io/en/latest/): Parameterizing, executing, and analyzing Jupyter Notebooks
- [interpret](https://pypi.org/project/interpret/): Interpretable model development

### Visualisation tools

- [Plotly](https://plotly.com/python/)
- [Seaborn](https://seaborn.pydata.org/)
- [ydata-profiling](https://docs.profiling.ydata.ai/latest/): Data profiling

### ML libraries

- [Scikit-Learn](https://scikit-learn.org/stable/index.html): Suite of commonly used algorithms
- [AutoTS](https://pypi.org/project/AutoTS/): Automated time series forecasting
- [XGBoost](https://xgboost.readthedocs.io/en/latest/python/python_intro.html) + [Optuna](https://optuna.org/): Powerful black-box method with automated hyperparameter optimization
- [Tensorflow and Keras](https://www.tensorflow.org/api_docs/python/tf): Deep learning and neural networks
- [Lifelines](https://lifelines.readthedocs.io/en/latest/): Survival analysis tools
