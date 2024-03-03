# Managing Software
Terms to know:
- `dpkg` is Ubuntu package manager
- `apt` (advanced package tool), frontend tool

## Sudo
Sudo is like a root command to add onto other commands 

Create a new directory 

`cd /usr/local/bin
sudo mkdir data` 

In this case I already have the direcory made so it returns 
```
sudo mkdir data
mkdir: cannot create directory ‘data’: File exists
```
Creating a file outside home directory 

`cd /srv
sudo touch data.csv`

## Apt commands

Update package list `sudo apt update`

Upgrade packages: `sudo apt upgrade` 

Search for packages: `apt search <package_name>` 

Show package details: `apt show <package_name>`

Install packages: `sudo apt install <package_name>` 

Remove packages: `sudo apt --purge remove <package_name>`

Autoremove packages, removes unsed ones: `sudo apt autoremove`

Clean package cache: `sudo apt clean`

**Apt search**

Does not require sudo command to start

Searches for specfic packages 
```
apt search tldr

Sorting... Done
Full Text Search... Done
libghc-tldr-dev/focal 0.4.0.1-1build2 amd64
  Haskell tldr client

libghc-tldr-doc/focal 0.4.0.1-1build2 all
  Haskell tldr client; documentation

libghc-tldr-prof/focal 0.4.0.1-1build2 amd64
  Haskell tldr client; profiling libraries

tldr/focal 0.4.0.1-1build2 amd64
  Haskell tldr client

tldr-py/focal 0.7.0-3 all
  Python client for tldr: simplified and community-driven man pages

```

**Apt show**

Show specfic info for a certain package 
```
apt show tldr

Package: tldr
Version: 0.4.0.1-1build2
Priority: optional
Section: universe/doc
Source: haskell-tldr
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Debian Haskell Group <pkg-haskell-maintainers@lists.alioth.debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 3013 kB
Depends: libatomic1 (>= 4.8), libc6 (>= 2.29), libffi7 (>= 3.3~20180313), libgmp10, git
Conflicts: tldr-py (<< 0.7.0-2~)
Homepage: https://github.com/psibi/tldr-hs#readme
Download-Size: 584 kB
APT-Sources: http://us-west4.gce.archive.ubuntu.com/ubuntu focal/universe amd64 Packages
Description: Haskell tldr client
 Haskell tldr client with support for updating and viewing tldr pages.
 .
 The TLDR pages are a community effort to simplify the beloved man
 pages with practical examples.  See https://tldr.sh/
```
**Sudo apt install**

Install the TLDR package

```
 sudo apt install tldr
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libatomic1
The following NEW packages will be installed:
  libatomic1 tldr
0 upgraded, 2 newly installed, 0 to remove and 3 not upgraded.
Need to get 593 kB of archives.
After this operation, 3059 kB of additional disk space will be used.
Do you want to continue? [Y/n] y

```
**Sudo apt remove**

Remove packages 

```
sudo apt --purge remove tldr
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following package was automatically installed and is no longer required:
  libatomic1
Use 'sudo apt autoremove' to remove it.
The following packages will be REMOVED:
  tldr*
0 upgraded, 0 newly installed, 1 to remove and 3 not upgraded.
After this operation, 3013 kB disk space will be freed.
Do you want to continue? [Y/n] 

```

**Auto remove packages**

Remove unused packages 

```
sudo apt autoremove
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  libatomic1
0 upgraded, 0 newly installed, 1 to remove and 3 not upgraded.
After this operation, 46.1 kB disk space will be freed.
Do you want to continue? [Y/n] 

```

Remove extra files 

`sudo apt clean`

# Library Search

- `yaz-client` is a command-line tool for information retrieval using the Z39.50 protocol, a standard for querying and retrieving bibliographic information in libraries.
- SRU (Search/Retrieve via URL) and SRW (Search/Retrieve Web service) are modern successors to Z39.50, facilitating web-based bibliographic record access.

## Yaz
Search for yaz
```
apt search yaz

Sorting... Done
Full Text Search... Done
libnet-z3950-zoom-perl/focal 1.30-2build1 amd64
  Perl extension implementing the ZOOM API for Information Retrieval via Z39.50
...
```
Learn about yaz package
```
apt show yaz

Package: yaz
Version: 5.28.0-1build2
Priority: optional
Section: universe/devel
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Vincent Danjean <vdanjean@debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 348 kB
Depends: libc6 (>= 2.14), libreadline8 (>= 6.0), libxml2 (>= 2.7.4), libyaz5 (>= 5.27.1)
Conflicts: yaz-runtime, yaz-ssl
Homepage: https://www.indexdata.com/resources/software/yaz/
Download-Size: 103 kB
APT-Manual-Installed: yes
APT-Sources: http://us-west4.gce.archive.ubuntu.com/ubuntu focal/universe amd64 Packages
Description: utilities for YAZ Z39.50 toolkit
 YAZ is a toolkit that allows you to develop software using the
 ANSI Z39.50/ISO23950 standard for information retrieval.
 .
 This package includes utility programs.
```
Install yaz
```
sudo apt install yaz
Reading package lists... Done
Building dependency tree       
Reading state information... Done
```
**Using Yaz**

Access yaz

`yaz-client`
  *^ starts new command line* `Z>`

Connect to UK lib service 
```
Z> open saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY
Connecting...OK.
Sent initrequest.
Connection accepted by v3 target.
ID     : 81
Name   : Aleph Server/GFS/YAZ
Version: ALEPH 20/1.1.1.1/2.1.32
Options: search present delSet triggerResourceCtrl scan sort extendedServices namedResultSets

```

## Documentation

To access yaz documentation run
`man yaz-client`

To access yaz documentation via web (more comprehensive)
[YAZ homepage](https://www.indexdata.com/resources/software/yaz/) 


## Queries

- Queries use PQN (Prefix Query Notation), structuring searches with operators preceding operands

**Examples**

Search for "information" and Library of Congress Subject Heading "library science"
```
yaz-client
Z> open saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY
Connecting...OK.
Sent initrequest.
Connection accepted by v3 target.
ID     : 81
Name   : Aleph Server/GFS/YAZ
Version: ALEPH 20/1.1.1.1/2.1.32
Options: search present delSet triggerResourceCtrl scan sort extendedServices namedResultSets
Elapsed: 0.123681
Z> find @and @attr 1=4 "information" @attr 1=21 "library science"
Sent searchRequest.
Received SearchResponse.
Search was a success.
Number of hits: 664, setno 1
records returned: 0
Elapsed: 1.123562
```
Command breakdown
```
Find @and @attr 1=4 "information" @attr 1=21 "library science"

Search w two criteria combined by AND SEARCH WHERE Title CONTAINS
"information" AND Subject IS "library science" Execute and display results
IF matches FOUND THEN display matches ELSE "No matches"

```
To show first record 
```
Z> show 1
Sent presentRequest (1+1)
```
Find subject headings "library science" and "philosophy"
```
Z> f @and @attr 1=21 "library science" @attr 1=21 "philosophy"
Sent searchRequest.
Received SearchResponse.
Search was a success.
Number of hits: 59, setno 1
records returned: 0
Elapsed: 1.231668
```
Command breakdown

```
f @and @attr 1=21 "library science" @attr 1=21 "philosophy"

Search for records w both specified subjects SEARCH WHERE Subject IS "library science" AND
Subject IS "philosophy" Execute and display results IF matches FOUND THEN display matches
ELSE "No matches"
```

Search for spefic name ex "Larry Mcmurty"

```
Z> f @attr 1=1 "mcmurtry, larry"
Sent searchRequest.
Received SearchResponse.
Search was a success.
Number of hits: 59, setno 2
records returned: 0
Elapsed: 0.699406

```

Search for "c programming language"

```
Z> f @attr 1=1016 "c programming language"
Sent searchRequest.
Received SearchResponse.
Search was a success.
Number of hits: 1637, setno 3
records returned: 0
Elapsed: 1.811768

```

