
Documentation for hwaf

# Introduction

This documentation explains how the Hwaf tools can be used whereas you are a client (user) of a software configured by Hwaf, or you are a software developper in a project configured using Hwaf, or you are managing a software base using Hwaf.
Parts of this documentation describe the architecture of the Hwaf tool, and a section list the detailed technical documents.

This documentation reflects in particular the conventions, usage adopted in the Atlas project, although most of the rules and recipes should be applied in other projects.

In addition there are in every section, some bits of comparisons with former recipes using the CMT tool. 

# Using hwaf as a software user

You want to use a piece of software that has been configured, produced and developped using Hwaf.

## Setting up Hwaf
## Where is your software 
## How to setup for running
## Queries onto the software base

# Using hwaf as a software developper

You want to contribute to a software base which is configured using Hwaf. 

## Setting up Hwaf

## Configuring the software base
### Selecting a work model

``hwaf`` supports multi-projects builds, where each project holds a number of interrelated packages. Projects have their own life, (with build and installation area).

Then the central tool in ``hwaf`` is the concept of the workarea, where locally checked out packages will live.

To create such a workarea:

```sh
$ cd dev
# create a workarea named 'work'
$ hwaf init work
$ cd work
```

When you create a workarea, you can instruct it to use the definitions
and objects defined by other projects, using the ``hwaf setup``
command:

```sh
$ cd work
$ hwaf setup -p /path/to/a/project/install
```

Simple projects don't need that:

```sh
$ cd work
$ hwaf setup
$ hwaf show setup
workarea=/home/binet/dev/work
cmtcfg=x86_64-archlinux-gcc47-opt
projects=
```

### Configure the workarea
We can run the ``configure`` command to test whether all
dependencies are installed and generate the bootstrap code to be able
to compile:

```sh
$ hwaf configure
Setting top to                           : /home/binet/dev/work 
Setting out to                           : /home/binet/dev/work/__build__ 
Manifest file                            : /home/binet/dev/work/.hwaf/local.conf 
Manifest file processing                 : ok 
Checking for 'g++' (c++ compiler)        : g++ 
Checking for 'gcc' (c compiler)          : gcc 
================================================================================
project                                  : work-0.0.1 
prefix                                   : install-area 
pkg dir                                  : src 
variant                                  : x86_64-archlinux-gcc47-opt 
arch                                     : x86_64 
OS                                       : archlinux 
compiler                                 : gcc47 
build-type                               : opt 
projects deps                            : None 
install-area                             : install-area 
njobs-max                                : 2 
================================================================================
[...]

```

## Creating a package
### A new package
### Get a package from existing sources
## Structure of a package
### Conventions for Atlas
## Constituents of a package
## Parameters of a package
### Defining a configuration parameter
### Variants & tags
## Declaring the dependencies
## Using the standard festures
## Adding new features
## Queries onto the software base
## Connecting to already installed (external) sofware

# Using hwaf as a Librarian

You want to manage a sofware base around the Hwaf concepts & tool.

## Installing Hwaf itself
## Setting up Hwaf
## Configuring the software base
### Defining a work model
## How to distribute your software
## Connection to the DCVS
## Import/export software
## Connecting to already installed sofware

# Hwaf architecture

## Management concepts
## The hwaf workflows
### Configure
### Build
### Install
### Run
## The specification languages
### Yaml
### Waf scripts

# Technical documentation


