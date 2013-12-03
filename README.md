Documentation for hwaf

# Introduction

This documentation explains how the Hwaf tools can be used whereas you are a client (user) of a software configured by Hwaf, or you are a software developper in a project configured using Hwaf, or you are managing a software base using Hwaf.
Parts of this documentation describe the architecture of the Hwaf tool, and a section list the detailed technical documents.

This documentation reflects in particular the conventions, usage adopted in the Atlas project, although most of the rules and recipes should be applied in other projects.

In addition there are in every section, some bits of comparisons with former recipes using the CMT tool. 

# Using hwaf as a software user

You want to use a piece of software that has been configured, produced and developped using Hwaf.

## Setting up `hwaf`

### Installing `hwaf` from sources
``hwaf`` is a ``Go`` binary produced by the [Go toolchain](http://golang.org).
So, if you have already the ``Go`` toolchain installed (see
[here](http://golang.org/doc/install.html) for instructions) you just have to
do:

```sh
$ go get github.com/hwaf/hwaf
```

to get the latest ``hwaf`` tool (and its ``git`` goodies) installed
and ready.


### Installing pre-packaged `hwaf` binaries

Packaged up binaries for ``hwaf`` are also available [here](http://cern.ch/hwaf/downloads/tar).
Untar under some directory like so (for linux 64b):

```sh
$ mkdir local
$ cd local
$ curl -L \
  http://cern.ch/hwaf/downloads/tar/hwaf-SOMEVERSION-linux-amd64.tar.gz \
  | tar zxf -
$ export HWAF_ROOT=`pwd`
$ export PATH=$HWAF_ROOT/bin:$PATH
```

### Using `hwaf` from `CERN-AFS`

Pre-packaged binaries of ``hwaf`` are also available on ``CERN-AFS``:

```sh
$ . /afs/cern.ch/atlas/project/hwaf/sw/install/latest/linux-amd64/setup-hwaf.sh
$ which hwaf
/afs/cern.ch/atlas/project/hwaf/sw/install/hwaf-20131202/linux-amd64/bin/hwaf
```

## Where is your software 

to be completed

## How to setup for running

to be completed

## Queries onto the software base

At the moment, a few queries have been implemented:

```sh
# list the parent project of the current project
$ hwaf show projects
project dependency list for [work] (#projs=0)
work
'show-projects' finished successfully (0.015s)

# list the dependencies of a given package
$ hwaf show pkg-uses mytools/mypkg
package dependency list for [mytools/mypkg] (#pkgs=0)
mytools/mypkg
'show-pkg-uses' finished successfully (0.015s)

# print the value of some flags: C++ compilation, link, shared-lib
$ hwaf show flags CXXFLAGS LINKFLAGS
CXXFLAGS=['-O2', '-m64']
LINKFLAGS=[]

# print the constituents of a project
$ hwaf show constituents
cxx-hello-world 
py-hello 
```

(to be continued)


# Using hwaf as a software developper

You want to contribute to a software base which is configured using Hwaf. 

## Setting up hwaf

to be completed

## Configuring the software base
### Selecting a work model

``hwaf`` supports multi-projects builds, where each project holds a number of interrelated packages. Projects have their own life (with specific build and installation areas).

Then the central tool in ``hwaf`` is the concept of the workarea where the current project resides. Locally checked out packages of this project will live.

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

By default, a workarea will hold
* a set of packages (each in its dedicated subdirectory)
* a common build area, meant tu receive the output of all build actions for all packages of the workarea.
* a common installation area
* a configuration script (a python script named hscript) automatically generated by the init command.

The hscript contains the steering mechanisms needed by hwaf to operate the various build, install, test actions in every package of the current project.

Although one may customize this script, generally speaking, only configuration specific scripts within each package need to be adpated. 

## Creating a package

Creating a package consists in adding a subdirectory inside the workarea.

### A new package

``hwaf`` has a subcommad to create a default package:

```sh
$ hwaf pkg help create
Usage: hwaf pkg create [options] <pkg-full-path>

create creates a new package in the current workarea.

ex:
 $ hwaf pkg create MyPath/MyPackage
 $ hwaf pkg create -script=yml MyPath/MyPackage
 $ hwaf pkg create -script=py  MyPath/MyPackage

options:
  -authors="": comma-separated list of authors for the new package
  -script="yml": type of the hwaf script to use (yml|py)
  -v=false: enable verbose output

$ hwaf pkg create MyDir/MyPackage

$ tree .
.
|-- local.conf
|-- src
|   `-- MyDir
|       `-- MyPackage
|           |-- MyPackage
|           |-- hscript.yml
|           `-- src
`-- wscript

5 directories, 3 files
```

This will create a package with name ``MyPackage`` under the directory ``MyDir``.
Notice this will create a package with a ``hscript.yml`` file.
One can also create a package with a ``hscript.py`` file by passing the ``-script=py`` option.

### Get a package from existing sources

to be completed

## Structure of a package

to be completed

### Conventions for Atlas

to be completed

## Constituents of a package

to be completed

## Parameters of a package

to be completed

### Defining a configuration parameter

to be completed

### Variants & tags

to be completed

## Declaring the dependencies

to be completed

## Using the standard festures

to be completed

## Adding new features

to be completed

## Queries onto the software base

to be completed

## Connecting to already installed (external) sofware

to be completed


# Using hwaf as a Librarian

You want to manage a sofware base around the Hwaf concepts & tool.

## Installing Hwaf itself

to be completed

## Setting up Hwaf

to be completed

## Configuring the software base

to be completed

### Defining a work model

to be completed

## How to distribute your software

to be completed

## Connection to the DCVS

to be completed

## Import/export software

to be completed

## Connecting to already installed sofware

to be completed


# Hwaf architecture

## Management concepts

to be completed

## The hwaf workflows

to be completed

### Configure

to be completed

### Build

to be completed

### Install

to be completed

### Run

to be completed

## The specification languages

to be completed

### Yaml

to be completed

### Waf scripts

to be completed


# Technical documentation


to be completed


