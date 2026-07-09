## Initial Mac Setup

### [Homebrew](https://brew.sh/)

Homebrew is a package manager for macOS. In other words, it is a tool that installs and updates software from the command line terminal. You can install packages via

brew install <name>

These packages are typically system-level, meaning they can oversee everything within your computer. 

A crucial package to download is git, which allows your work to sync with github.

```
brew install git
```


wget is often used to download files or databases
```
brew install wget
```

tmux (terminal multi-plexer) lets you run sessions even after you have disconnected.
```
brew install tmux
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
