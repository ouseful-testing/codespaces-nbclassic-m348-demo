# TM351 Environment in Github Codespaces Demo

Demo of running an OU maintained Docker container as the computational environment.

Note that the workspace can be slow to build (watch the logs!) and once the JupyterLab environment has loaded, it may take a little while for the kernel to become available for the first loaded notebook. (Try restarting it after a while, or stopping and closing the notebook, then opning it again, if the kernel does not seem to be responsive).

*I've also noticed JupyterLab somtimes gets a bit stuck; hard refreshing the browser with devtools open to clear the cache generally fixes it...*

## End-User Rationale

The demo is interesting for several reasons:

- a custom container can be provided that defines a complex computational environment for use in the Codespace. In the current example, the container is a container used in the Open University module *TM351 Data Management and Analysis*. This environment includes:
  - a PostgreSQL server with preconfigured user accounts;
  - a MongoDB server seeded with a several data collections;
  - __we can deliver a complex computational environment to students that we can update as required by updating the original Docker image__
  
- Codespaces provide a generous amount of free hosted compute hours per month, meaning an install free user experience;
  - __students can use the Codespaces environment for free without any hosting burden on, or costs to, the OU__

- the editing environment is separate from the containerised computational environment. Codespaces can be used to provide install free, customisable, browser based VS Code and JupyterLab environments:
  - the VS Code editor can be customised by installing additional extensions via the `devcontainer.json` file;
  - the JupyterLab editing environment can be customised by installing JuptyerLab extensions via the `requirements.txt` file;
  - __we can separate concerns of delivering a customised computational environment (via the Docker image) and a customised user editing environment (via `.devcontainer` config files in the repo)__

- file edits can be persisted in a Github repository using the VS Code and JupyterLab git extensions. (Modified files are persisted in the container and can also be published to a new branch);
  - __provides a natural rationale for getting students into the habit of using version control / git__
  
- *the JupyterLab environment does supports a local file access extension but this doesn't appear to work in this context at the moment...*

- language pack extensions can be added to the JupyterLab environment; the current environment includes French and Chinese language packs, along with English (the default); change language from the JupyterLab `Settings > Language` menu option;
  - __we can support localised language packs for foreign students, or locally customised labels as required; users can install additional language packs themselves__

*The full TM351 environment includes a proxied OpenRefine server, although this seems to knock the Codespace container over. I think this is because OpenRefine is a resource heavy Java application that seems happiest with at least 4GB of memory available.*

### Using the JupyterLab UI

We can specify the default Codespaces editor to be JuptyerLab from the Github user settings page:

<img width="789" alt="image" src="https://user-images.githubusercontent.com/82988/234049241-d4f12077-1c36-4495-977f-f5f95a0dcc57.png">

Create a repository from the *Use this template* button:

<img width="1047" alt="image" src="https://github.com/ouseful-testing/codespaces-jupyter-tm351/assets/82988/98470329-79bb-4e3e-b6a0-dd9b5b0c9efa">

To access the environment:

- create a Github account;
- click on *Use this template*;
- create a private repository based on the template;
- open a new Codespace from your own repository (see above for how to ensure that JupyterLab is the default launch UI).


__Note that it may take several minutes for the container to be built the first time you use it or if you delete the workspace and create a new one. If you stop a workspace and restart it at a later time, the set-up should be quicker.__

When the Codespace container is built, the JupyterLab UI should be automatically opened in your browser with access to that environment.

If you get something like this:

<img width="1255" alt="image" src="https://user-images.githubusercontent.com/82988/234068267-f65fcc61-f18d-49e8-88cd-ba36d4dbdf1f.png">

then hard refresh the browser page.

The intial display may appear a bit broken... Try clicking things to reset the view...

<img width="1061" alt="image" src="https://user-images.githubusercontent.com/82988/234069091-a3c3f024-d92b-4bb8-8077-c484795a0135.png">

A wide variety of JupyterLab extensions are preinstalled in the environment, including a branding pack and cell execution status indicators.

<img width="1254" alt="image" src="https://user-images.githubusercontent.com/82988/234067070-205b4935-52f6-4560-9eb6-e5b161033056.png">

[Empinken styling](https://github.com/innovationOUtside/jupyterlab_empinken_extension) is supported, and a growing number of MyST styling features are supported by the [`jupyerlab-myst` extension](https://github.com/executablebooks/jupyterlab-myst).

<img width="664" alt="image" src="https://user-images.githubusercontent.com/82988/234069968-407e3392-df98-450a-a1c4-b36f12f77e75.png">

The pre-installed `jupyterlab-git` extension allows you to commit and push changes back to the code repository.

<img width="1260" alt="image" src="https://user-images.githubusercontent.com/82988/234066314-4c1089ab-a592-403f-b72a-792d3e454ca5.png">

The extension also includes a *diff*er, so you can inspect changes you have made to a file, but not committed:

<img width="1227" alt="image" src="https://user-images.githubusercontent.com/82988/234078676-0656a2df-236e-4002-a9c4-d958ad72d8c0.png">

To upload notebooks, students can download a (controlled) release from the VLE, unzip them, and then drag and drop the notebook directory onto their Github repo page to upload them to the repo. If their Codespace already exists, they should be able to use the git tools to synch the uploaded files into their workspace.

<img width="1009" alt="image" src="https://user-images.githubusercontent.com/82988/234077775-c52e87dc-9a8f-4ff8-b292-9eda211b9a09.png">

When using the devcontainer locally by opening the cloned repo directory using VS Code, it seems that the dev containr does not install its own JupyterLab server? However, there is the JupyterLab environment that we built into the original TM351 container, and it seems we can run that by issuing the `jupytr lab` command from the terminal inside a VS Code environment attached to the container:

<img width="776" alt="image" src="https://user-images.githubusercontent.com/82988/234289794-d5b1bf2f-c867-4939-8819-3f87d07f7cd5.png">


### Using the VS Code UI

If we choose to open the Codespace in the browser (which is to say, VS Code in the browser), or in VS Code (which is to say, VS Code running locally), or if we clone the repo and open the directory in a local version of VS Code with the [*Dev Containers* extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) installed, we can run the code cells by selecting the `/usr/bin/python3` environment:

<img width="945" alt="image" src="https://user-images.githubusercontent.com/82988/234274313-1176e6c9-067f-4784-b4e3-0d9e5cfb8b6d.png">

## Technical Notes

To customise the JupyterLab environment published by the devcontainer, we install the required JupyterLab extensions from the `requirements.txt` file included in this repo: `"updateContentCommand": "python3 -m pip install -r requirements.txt"`

The container used in the demo [`mmh352/tm351:23j.0b8`](https://hub.docker.com/r/mmh352/tm351/tags) is a standalone container that includea all the required services packages and applications.

The container features first-run as well as on-start procedures:

- *first run*: the first run process includes a [step](https://github.com/OpenComputingLab/vce-jupyter-stacks/blob/main/tm351-notebook-jh/start_jh_extras) to copy the seeded database db files, as shipped within the original container, to a user mounted location in order the persist any changes that are made to the database to a persistent location outside the container (either the user's desktop for the local VCE, or the persistent user storage area in the OU hosted VCE).
- [*start procedure*](https://github.com/OpenComputingLab/vce-jupyter-stacks/blob/main/tm351-monolith/start): the start procedure performs various seeding checks and calls first run routines as required, and then starts the PostgreSQL and MongoDB services.

In the `devcontainer.json`, we replicate the original container start procedure in the following way:

- first run: `"postCreateCommand": "sudo /var/startup/start_jh_extras"`
- on start: `"postStartCommand": "sudo service postgresql restart && sudo mongod --fork --logpath /dev/stdout --dbpath ${MONGO_DB_PATH}"`

We hold the launch of the UI until the environment has been properly seeded and the `postStartCommand` has started the database services.

__Updates to the PostgreSQL and MongoDB databases are not persisted outsude the container.__

