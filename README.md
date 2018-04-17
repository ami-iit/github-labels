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

`$ sudo apt-get install npm`

Then you need to install the following two packages
* [github-labels](https://github.com/popomore/github-labels)
* [copy-github-labels-cli](https://github.com/jvandemo/copy-github-labels-cli)

**NOTE**: You can manage the labels of repositories to which you have write access! Please ensure it before proceeding further.

The package [github-labels](https://github.com/popomore/github-labels) lets you to add labels to your github repository from `.json` file directly using

`$ labels -c <file> -f <github_user>/<repo_name> -t <token>`

e.g. `$ labels -c github-labels.json -f loc2/my-new-awesome-repo -t ${GITHUB_TOKEN}`

**NOTE**: 

* The option `-f` is force option which will delete all existing labels.

* If some of the labels in the `.json` file are already used in your new repo, the above command will throw an error. Do not worry about it, the rest of the labels will be copied correctly. Please double check this! 

The package [copy-github-labels-cli](https://github.com/jvandemo/copy-github-labels-cli) lets you to copy the labels from one repository to another repository.

To copy the labels from one repository to another repository use

`$ copy-github-labels -t <token> <source-repo> <destination-repo>`

e.g. `$ copy-github-labels -t ${GITHUB_TOKEN} loc2/github-labels loc2/my-awesome-new-repo`

**NOTE**:
* If some of the labels in the `.json` file are already used in your new repo, the above command will throw `Unknown label: failed (Validation Failed)` error for all the conflicting labels. Do not worry about it, the rest of the labels will be copied correctly. Please double check this!
