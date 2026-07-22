## Initial Mac Setup

### [Homebrew](https://brew.sh/)

Homebrew is a package manager for macOS. In other words, it is a tool that installs and updates software from the command line terminal. You can install packages via

brew install <name>

These packages are typically system-level, meaning they can oversee everything within your computer. Besdies a few system-level packages, we would prefer to download enviornment-level pacakges using Conda

```
brew install git #work in sync with github
brew insall wget #Download online files/databases
brew install tmux #Terminal MUlti-Plexer) lets you run sessions even after you have disconnected.
```


To "kick off" jobs within dogen:
```
ssh dogen
tmux new -s <name>
# The command needed, such as waafle_search .... --threads 8
# press Ctrl-b, then d
# now you can log out safely
```
To list active sessions,
```
tmux ls
```
