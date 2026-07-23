### Baqlava

Note: Use micromamba v1.4.3

[baqlava_env.yaml]
```yaml
name: baqlava_env
channels:
  - conda-forge
  - bioconda
  - biobakery
dependencies:
  - python=3.12
  - humann=3.9
  - anadama2
  - pip
  - pip:
      - baqlava
```

   
### Waafle:

```yaml
name: waafle_env
channels:
  - conda-forge
  - bioconda
  - biobakery
dependencies:
  - waafle

### Megahit
name: megahit_env
channels:
  - conda-forge
  - bioconda
  - biobakery
dependencies:
  - megahit
```