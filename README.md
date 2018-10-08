# github-labels
The repo contains all the GitHub issue labels we use within our organisation. The labels are stored in [all_github_labels.json](https://github.com/loc2/github-labels/blob/master/all_github_labels.json) and also stored in `.json` files for specific [categories](https://github.com/loc2/github-labels/tree/master/label-categories).

## How-to
A github token provides API access to npm packages that help to manage github issue labels. You can generate a personal token follow [this guide](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/).

Once a token is generated add the following lines to the `.bashrc`

`export GITHUB_USER="<USERNAME>"`

`export GITHUB_TOKEN="<TOKEN>"`

Then source it!

`$ source ~/.bashrc`

you need to first install `npm` package manager

`$ sudo apt-get install nodejs npm`

**NOTE:** You may get the following error while installing `npm`

```
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
npm : Depends: node-gyp (>= 0.10.9) but it is not going to be 
installed
E: Unable to correct problems, you have held broken packages.
```
In this case use the following steps:

- Install the nvm (node version manager)

`$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash`

`$ nvm install node`

Then you need to install the following two packages
* [github-labels](https://github.com/popomore/github-labels)
* [copy-github-labels-cli](https://github.com/jvandemo/copy-github-labels-cli)

**NOTE**: You can manage the labels of repositories to which you have write access! Please ensure it before proceeding further.

The package [github-labels](https://github.com/popomore/github-labels) lets you to add labels to your github repository from `.json` file directly using

`$ labels -c <file> -f <github_user>/<repo_name> -t <token>`

e.g. `$ labels -c github-labels.json -f loc2/my-new-awesome-repo -t ${GITHUB_TOKEN}`

**NOTE**: 

* The option `-f` is force option which will delete all existing labels. A newly created repo contains some default labels and using this option will delete them!

* If some of the labels in the `.json` file are already used in your new repo, the above command will throw an error. Do not worry about it, the rest of the labels will be copied correctly. Please double check this! 

The package [copy-github-labels-cli](https://github.com/jvandemo/copy-github-labels-cli) lets you to copy the labels from one repository to another repository.

To copy the labels from one repository to another repository use

`$ copy-github-labels -t <token> <source-repo> <destination-repo>`

e.g. `$ copy-github-labels -t ${GITHUB_TOKEN} loc2/github-labels loc2/my-awesome-new-repo`

**NOTE**:

* If the above command gives `/usr/bin/env: node: No such file or directory` error run the following command. This is to create a symlink to the package installed through `npm` package manager 

    `sudo ln -fs /usr/bin/nodejs /usr/local/bin/node`

* If you are following this method the new labels are created alongside the existing labels. 

* If some of the labels in the `.json` file are already used in your new repo, the above command will throw `Unknown label: failed (Validation Failed)` error for all the conflicting labels. Do not worry about it, the rest of the labels will be copied correctly. Please double check this!

