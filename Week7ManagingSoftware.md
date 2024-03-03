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

## Installing yaz

1. Search for yaz: `apt search yaz`
2. Install yaz: `sudo apt install yaz`

## Documentation

- Access documentation via `man yaz-client` or visit [YAZ homepage](https://www.indexdata.com/resources/software/yaz/) for comprehensive information.

## Using yaz

- Start `yaz-client`: `yaz-client`
- Connect to a library's OPAC: `open <server_address>`

## Queries

- Queries use Prefix Query Notation (PQN), structuring searches with operators preceding operands.
- Example: To search titles with the word 'information' and the subject 'library science': `find @and @attr 1=4 "information" @attr 1=21 "library science"`
- Use the `show` command to display search results: `show <record_number>`


### Overview/Reflection

Z39.50, SRU, and SRW protocols, along with tools like `yaz-client`, facilitate direct command-line access to digital library searches and bibliographic data retrieval.

