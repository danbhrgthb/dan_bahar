### Tmux (Terminal Multi-Plexer)

Tmux allows for multiple terminal sessions to run simultaneously. It is also very useful for "kicking off" jobs within dogen, which means that the job will run even after you disconnect from dogen.

To kick off jobs within dogen:

```
ssh dogen

tmux new -s <name>
# The command needed, such as waafle_search .... --threads 8
# press Ctrl-b, then d
# now you can log out safely
```

To list active sessions, ```tmux ls```
