# bowl1 test configuration

## Introduction

This is a self-contained MOM5 test configuration. All required input 
files are committed to the repository and located in the `INPUT` directory.

## Compiling the model

This configuration requires a MOM5 solo build, i.e. no sea-ice or BGC
coupled components.

Using the [ACCESS-NRI spack configuration at NCI](https://docs.access-hive.org.au/getting_started/spack/) 
this is a known good [spack environment to create](https://docs.access-hive.org.au/models/build_a_model/build_source_code/?h=spack+env#create-a-spack-development-environment) for MOM5:
```yaml
# This is a Spack Environment file.
# 
# It describes a set of packages to be installed, along with
# configuration settings.
spack:
  specs:
  - mom5@mom_solo
  packages:
    # Indirect dependencies
    netcdf-c:
      require:
      - '@4.9.2'
    netcdf-fortran:
      require:
      - '@4.6.1'
    openmpi:
      require:
      - '@4.1.7'
    c:
      prefer:
      - 'intel-oneapi-compilers-classic'
    cxx:
      prefer:
      - 'intel-oneapi-compilers-classic'
    fortran:
      require:
      - 'intel-oneapi-compilers-classic'
    all:
      prefer:
      - 'target=x86_64_v4'
  view: true
  concretizer:
    unify: true
```

But it is also possible to compile the model directly using the build system.

## Running the configuration

There is a `config.yaml` file so the configuration can be run with 
[payu model run tool](https://github.com/payu-org/payu), but it should
also be possible to simply run a MOM5 solo executable in the directory
where this repo is cloned, as all configuration files are present, and the
model defaults to reading inputs from an `INPUT` directory.

If using payu the path to the executable needs to be modified in the 
`config.yaml`.

