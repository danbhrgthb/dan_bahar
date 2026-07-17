## Conda

Conda is a package manager (like [Homebrew](07072026%20Initial%20mac%20setup.md#homebrew) and environment manager. Like Homebrew, it installs software; but it can install software within separate, independent workspaces that can't interfere with anything else. For example, we can use Python version 3.10 in one workspace while using Python 2.5 in a different workspace, without any conflicts.


## Installing Conda
```
brew install miniconda
conda init zsh
source ~/.zshrc
```
The last line is used to reload your terminal, which allows for changes to take affect immediately.

## Using conda

Because you have installed conda, you created different workspaces/enviornments within your computer. The default one is named base. You can tell which environment you're in by looking at the beginning of your terminal prompt

To create a new enviornment,
```
conda create -n baqlava_env
```
The -n flag is to enter a name for your envionrment (in this case, the name is baqlava_env).

To enter an eneviornment,
```
conda activate baqlava_env
```
To leave an enviornment and return to (base),
```
conda deactivate
```
