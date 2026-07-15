# Baqlava and Humann installation on dogen - Troubleshooting Report

Goal: Install HUMAnN, AnADAMA2, and BaqLaVa on the dogen server (via micromamba) to run the BaqLaVa viral-profiling pipeline.

Conclusion: The install is blocked by a bug in package manager micromamba 2.8.1 (alias of conda), not by our commands or a missing package.

## The code and error in question

```
conda create -n baqlava_env "python=3.10" humann -c conda-forge -c bioconda -c biobakery
conda activate baqlava_env
```

```
error    libmamba Could not solve for environment specs
    The following packages are incompatible
    └─ humann =* * is not installable because there are no viable options
       ├─ humann [3.0.0|3.0.1|...|4.0.0a1] would require
       │  └─ metaphlan =* * but there are no viable options
       │     ├─ metaphlan [4.1.1|4.2.0|...|4.2.4] would require
       │     │  └─ h5py =* *, which does not exist (perhaps a missing channel);
       │     ├─ metaphlan 4.1.2 would require
       │     │  └─ matplotlib-base <3.9.0 *, which does not exist (perhaps a missing channel);
       │     ├─ metaphlan [2.8.1|3.0|...|4.1.0] would require
       │     │  └─ matplotlib-base =* *, which does not exist (perhaps a missing channel);
       │     └─ metaphlan 2.8.1 would require
       │        └─ matplotlib-base >=2.0,<3.0 *, which does not exist (perhaps a missing channel);
       ├─ humann [3.0.0|3.0.0.alpha.1|...|3.9] would require
       │  └─ metaphlan [>=3.0 *|>=3.0.0.alpha *|>=3.1 *|>=4.0 *], which cannot be installed (as previously explained);
       └─ humann 3.1.1 would require
          └─ metaphlan =3.1.0 *, which cannot be installed (as previously explained).
```

## Overview

micromamba 2.8.1 uses a "sharded" package index rather than downloading each online channel's full catalog. Therefore, micromamba fetches only tiny fragments of channels. I believe that the sharded package indexing is the root problem behind this. The sharded indexing process accidentally drops certain packages, some of which are humann dependencies. The installer believes that these packages (i.e. h5py) are missing, so it gives up.

## What was tried (and failed)

**1. Updated micromamba**

No change as it was already most recent version 2.8.1

**2. Fix channels + flexible priority**

```
conda config list
```
Output:
```
channels:
  - conda-forge
  - bioconda
  - biobakery
repodata_use_zst: true
channel_priority: flexible
```

Although the channels loaded and the flexibility was changed, humann did not download properly.

**3. Name the dropped packages explicitly when attempting to install humann (h5py, matplotlib-base, pandas, …), kind of like whack-a-mole**

Every time one was fixed, another missing package popped up, so this did not work.

**4. Removing the humann version constraint** also did not work, with the same packages (h5py) being "missing"

## Why I believe it is a bug

1. `conda search -c conda-forge h5py` can find h5py. If it were actually missing from the channel, it would not show up.

2. The packages only disappear if they are dependencies. When the packages are explicitly named, they execute fine. Therefore, it is not a problem with the package itself but rather the installer failing to capture crucial packages.



At this point in the process, I thought that the sharded indexing method could potentially be dropping files. So, I tried to force micromamba to download each channel's full catalog rather than using sharded indexing. 
I found out that sharded indexing uses compressed files for efficiency. So, I attempted to make the installer only use un-compressed files via `repodata_use_zst false`, thinking that micromamba would be forced to not use sharding.

```
conda config list
```
Output:
```
channels:
  - conda-forge
  - bioconda
  - biobakery
repodata_use_zst: false
channel_priority: flexible
```

However, even after doing so, micromamba was still using sharded indexing, somehow, and the same error occurred.
