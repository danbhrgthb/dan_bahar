## Multithreading

A thread is a single stream of instructions being carried out. "Multi-threaded" means a program can split its work into several parallel threads that run at the same time across multiple CPU (“brain of the computer”) cores (units). This will help run commands faster across multiple CPU cores.

In other words, normally, the code is “single-threaded,” meaning that one thread uses one core, and the other cores sit there doing nothing. However, following this protocol will get the other idle threads to help run commands. This is particularly important for complex profiling tools like bowtie2.

Most tools expose a flag to set the number of threads (i.e. bowtie2 uses -p):
```
bowtie2 -p 8 (...command)
```

This tells bowtie2 to use 8 threads rather than 1.

Make sure to pick a thread count that is BELOW your core count. Find out your core count as follows:
```
brew install coreutils

nproc
```
