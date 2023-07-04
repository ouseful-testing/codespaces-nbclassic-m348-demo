# M348 Environment in Github Codespaces Demo

Demo of running an OU maintained Docker container as the computational environment (requires GitHub account).

To run:

- (clone this repository)
- from the repository Code / Codespaces menu, launche a new Codespace with a VS Code user interface
- run the notebooks in the VS Code interface

Currently broken:

- when the Codespace has loaded, from the VS Code terminal, tun the command: `start.sh' [WORKS]
- a notebook server should start running, and you a pop-up should appear offering to *Open in Browser*; click the button, and access the notebook server (use the password/token `M348-23J`); note - it may take soem time to open / open a notebook; [WORKS]
- run the notebook code cells [BROKEN - KERNEL ERROR]

## End-User Rationale

The demo is interesting for several reasons:

- a custom container can be provided that defines a complex computational environment for use in the Codespace. In the current example, the container is a container used in the Open University module *M348*. This environment includes:
  - a classic Jupyter notebook server, customised using off-the-shel extensions;
  - an R environment with required packages pre-installed;
  - __we can deliver a complex computational environment to students that we can update as required by updating the original Docker image__
  
- Codespaces provide a generous amount of free hosted compute hours per month, meaning an install free user experience;
  - __students can use the Codespaces environment for free without any hosting burden on, or costs to, the OU__

- the editing environment is separate from the containerised computational environment. Codespaces can be used to provide install free, customisable, browser based VS Code and nbclassic Jupyter notebook environments:
  - the VS Code editor can be customised by installing additional extensions via the `devcontainer.json` file;
  - __we can separate concerns of delivering a customised computational environment (via the Docker image) and a customised user editing environment (via `.devcontainer` config files in the repo)__

- file edits can be persisted in a Github repository using the VS Code git extension. (Modified files are persisted in the container and can also be published to a new branch);
  - __provides a natural rationale for getting students into the habit of using version control / git__
