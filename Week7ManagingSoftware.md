# Managing Software

Linux distributions typically employ a package manager to manage software installations, upgrades, and uninstalls. Ubuntu uses `dpkg` as its package manager with `apt` (advanced package tool) as a frontend.

## Using sudo

- `sudo` allows executing commands as another user, typically the superuser (root), to perform administrative tasks.
- Not all users can use `sudo`; they must belong to the `sudo` group or, on Google Cloud Platform (GCP), the `google-sudoers` group.
- Basic `sudo` syntax: Prepend `sudo` to commands that require superuser privileges.

## apt Commands

- Update package list `sudo apt update`
- **Upgrade packages: `sudo apt upgrade` - Upgrades all upgradable packages.
- **Search for packages**: `apt search <package_name>` - Finds packages in the repositories.
- **Show package details**: `apt show <package_name>` - Displays detailed information about a package.
- **Install packages**: `sudo apt install <package_name>` - Installs a new package.
- **Remove packages**: `sudo apt --purge remove <package_name>` - Removes a package and its configuration files.
- **Autoremove packages**: `sudo apt autoremove` - Removes unused packages and dependencies.
- **Clean package cache**: `sudo apt clean` - Clears out the local repository of retrieved package files.

## Conclusion

The `apt` command suite simplifies software management on Ubuntu systems, providing straightforward commands for updating, installing, and removing software.

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

### Conclusion

Z39.50, SRU, and SRW protocols, along with tools like `yaz-client`, facilitate direct command-line access to digital library searches and bibliographic data retrieval.

