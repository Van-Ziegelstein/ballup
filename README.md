# Ballup
Bash script to create tarballs of a system.


## Purpose
This is a rudimentary script to perform system backups with [tar](https://www.gnu.org/software/tar/). It is intended for situations where a simple
rsync mirror won't cut it, either because a degree of compression is desired or because the backup media's filesystem doesn't support
Unix file permissions.

The script supports the standard compression algorithms and their multithreaded implementations:

* [gzip](https://www.gnu.org/software/gzip/)/[pigz](https://www.zlib.net/pigz/)
* [bzip2](https://sourceware.org/bzip2/)/[pbzip2](http://compression.ca/pbzip2/)
* [xz](https://tukaani.org/xz/)/[pixz](https://github.com/vasi/pixz)

## Usage
There are two backup types:

#### --full
Backup the entire system, excluding the following directories:

* `/proc`
* `/run`
* `/sys`
* `/tmp`
* `/dev`
* `/mnt`

Command format: 
`./ballup --full [ --path </path/to/archive> ] [ --algo <gzip|bzip|xz> ]`

#### --custom
Backup the system, excluding the same directories like in `--full` mode and additionally those 
matching the patterns in a user supplied file.

Command format:
`./ballup --custom [ </path/to/exclude-file> ] [ --path </path/to/archive> ] [ --algo <gzip|bzip|xz> ]`

The paths in `exclude-file` can contain wildcards. A sample file is provided with this repository. If the user doesn't
explicitly supply one, then the script will look for a file named "ballup_exclude" in the current directory.

#### Options
* `--path </path/to/archive>`: The location where the tarball should be created. The default is the current working directory. 
* `--algo <gzip|bzip|xz>`: The compression algorithm to use. The script will first check for the presence of a multithreaded
implementation and then for a standard one. By default, gzip is used.

## Limitations
* This utility is designed for Unix systems.
* With both operations root privileges may be required to access certain directories.

## Authors
**Van Ziegelstein** - Creator and Maintainer

## License
This abomination is licensed under the [MIT License](LICENSE).
