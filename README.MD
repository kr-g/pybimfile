
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)


# pybimfile - before image file (BIM File) - copy on write

`pybimfile` implements [`copy-on-write`](https://en.wikipedia.org/wiki/Copy-on-write) 
for file based resources

before a change to a file is written all changes are recorded in another file.


# memory / file layout

## header

| name | size (bytes) | description |
| --- | --- | --- | 
| blen | xpos | original size of file prior changes |
| mark | xpos | 0xdeafbeef as start marker |
| magick | 4 | 0xdeafbeef as magic marker |

## change record

| name | size / value | description |
| --- | --- | --- | 
| fpos | xpos | pointer to file change |
| blen | xpos | size of change segment |
| magick | 4 | 0xdeafbeef as magic marker |

a list of change records is stored as continuously stream after header


## limitation

- xpos (default) == 8 bytes ==> 2**(8*8) 
== 18.446.744.073.709.551.616 bytes total file size (default)
- the default can be changed by creating `BeforeImageFile` with a different `link_size`
- 

# remarks

this module is derived (refactored) from another tool by myself named `LargeFileGuard` in 
[`pyfileguard`](https://github.com/kr-g/pyfileguard) and intendend to be used together with
[`pyheapfile`](https://github.com/kr-g/pyheapfile/) related software modules


# Platform

Tested on Python3, and Linux.


# development status

alpha state.
the API or logical call flow might change without prior notice.

read [`CHANGELOG`](https://github.com/kr-g/pybimfile/blob/main/CHANGELOG.MD)
for latest, or upcoming news.


# installation
    
available on pypi. install with:

    python3 -m pip install pybimfile
    
