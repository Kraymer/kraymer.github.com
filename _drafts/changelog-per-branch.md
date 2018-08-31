---
title: [git/fabric] How to maintain a sane changelog across branches when using the Gitflow workflow
dropcaps: false
published: true
draft: true
tags:
- python
---
Workflow to maintain one changelog for each branch `hotfix` and `develop` and one consolidated.
The idea is to have an ongoing changelog (for next release) specific for each branch to avoid conflicts when editing, and automatically dump contents from these file to a consolidated global changelog.md at deploy time.

# Repository files organization

Changelogs are written in markdown format : easy to edit and easy to make it look nice on slack.
I don't like to pollute the root of my django repository so I put the ongoing changelogs in `<DJANGO_ROOT>/fab` folder, as the changelogs are ultimately related to deploys hence to fabric.
So we have :

~~~~
CHANGELOG.md
fab/
├── develop/
│   └── ONGOING.md
└── hotfix/
    └── ONGOING.md
~~~

An ONGOING file contains the changelog of what will be shipped in the next release of the branch. Its structure follows https://keepachangelog.com/en/1.0.0/ instructions :

~~~
### Added
- item 1
- item 2

### Fixed
- item 3
~~~

The CHANGELOG file is a concatenation of ONGOING contents prefixed by release version and date :

~~~
# [1.3.0] - 2018-08-31 11:37

### Added
- item 1
- item 2

### Fixed
- item 3

# [1.2.4] - 2018-08-30 17:45

### Changed
- item 1
~~~

# Editing files

ONGOING.md are edited by developer when pushing their changes to the branch.
Parallel development in hotfix and develop branches does not provoke git conflicts as ONGOING.md are branch specific.
The editing of CHANGELOG.md is more interesting as it is a fully automated process.

TO CONTINUE...
