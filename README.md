# Quick devcontainer setup for R

# Sources

- https://jamesgoldie.dev/writing/dev-containers-in-r/
- https://github.com/revodavid/devcontainers-r
- https://rocker-project.org/images/devcontainer/images.html

# How to

- install dev containers extension in VSCode
- (Ctrl+Shift+P) -> Add devcontainer configuration files to start GUI helper
- choose to add either in a project (to commit it) or in a user folder (it will be in `$HOME/.config/Code/User/globalStorage/ms-vscode-remote.remote-containers/configs/<proj_name>/.devcontainer/devcontainer.json`)
- click on show more templates - search for r - choose either base r (r-ver) or r-tidyverse image depending on your needs
- additionally, click on add features: renv-cache (it will add `"features": {"ghcr.io/rocker-org/devcontainer-features/renv-cache:0": {}	}`)
- finish and modify `.devcontainer.json` by hand:
    - add R packages to install (use \ to escape quotes), e.g. `"postCreateCommand": "R -q -e 'renv::install(\"bioc::txdbmaker\")'"`
    - mount path to you renv cache and additional data folders:
    ```json
    // path to renv cache in devcontainer
    "remoteEnv": {
        "RENV_PATHS_CACHE": "/renv/cache"
        },
    // Mount renv cache from default location on host
    "mounts": [
        "source=${localEnv:HOME}/.cache/R/renv/cache/,target=/renv/cache,type=bind",
    // Mount another data folder, if needed
		"source=${localEnv:HOME}/path/to/data/,target=/workspaces/data,type=bind" //mount data folder
    ]
    ```
- if there is no pop-up to reopen the folder in a container, use the command palette (Ctrl+Shift+P) and select "Dev Containers: Reopen in Container"