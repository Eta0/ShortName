# ShortName

Python command-line utility to view and modify
[8.3-style short file names](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file#short-vs-long-names)
on Windows, with no dependencies.

## Table of Contents

- [What Is This?](#what-is-this)
- [Setup](#setup)
  - [As a Script](#as-a-script)
  - [Optional Installation](#optional-installation)
- [Usage](#usage)
  - [View the Short Name of a File](#view-the-short-name-of-a-file)
  - [Set the Short Name of a File](#set-the-short-name-of-a-file)
- [License](#license)

## What Is This?

Files with sufficiently long names on Windows may have a second, shorter, hidden name called an
[8.3 alias](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file#short-vs-long-names).
They are usually automatically generated, but can be set manually as well.
This tool allows you to [view](#view-the-short-name-of-a-file) and [change](#set-the-short-name-of-a-file)
those aliases.

For example, you may have a file named `some_long_file_name.txt`.
With ShortName, you can run:

```cmd
python ShortName.py set some_long_file_name.txt short.txt
```

And now `some_long_file_name.txt` has the hidden alias `short.txt`.

If the full path to `some_long_file_name.txt` is `C:\Files\some_long_file_name.txt`,
you can now refer to it almost everywhere as `C:\Files\short.txt` as well;
`notepad C:\Files\short.txt` will open the same file as `notepad C:\Files\some_long_file_name.txt`.

## Setup

You can run ShortName either as a single-file script `ShortName.py`,
or install it to run it more easily from anywhere.

Regardless of the method, you first need to [install Python 3](https://www.python.org/downloads/) if you don't have it.

### As a Script

- [Download `ShortName.py`](https://raw.githubusercontent.com/Eta0/ShortName/main/ShortName.py)

No further installation is required, as it has no dependencies. You can use it immediately as a script, e.g.:

```cmd
python ShortName.py get .\some_long_file_name.txt
```

### Optional Installation

If you wish to install ShortName—for example, to invoke it from anywhere—you can run:

```cmd
python -m pip install ShortName
```
To install [ShortName via PyPI](https://pypi.org/project/ShortName).

Alternatively, you can:

1. [Download the ShortName repository](https://github.com/Eta0/ShortName/archive/refs/heads/main.zip)
2. Unzip it
3. Run `python -m pip install <path to unzipped directory>`

Regardless of which of installation method you choose, you should then be able to invoke `ShortName` from anywhere,
in either of the following two ways:

1. `python -m ShortName get .\some_long_file_name.txt`, or
2. `ShortName get .\some_long_file_name.txt`

To uninstall it, run:

```cmd
python -m pip uninstall ShortName
```

## Usage

ShortName has two commands, `get` and `set`, to either view or modify the short name of a file, respectively.

You can also run `python ShortName.py --help` for usage information.

### View the short name of a file

The command to view the short name of a file is `python ShortName.py get FILE`.

Example usage:

```cmd
python ShortName.py get .\some_long_file_name.txt
```

Example output:

```
.\SOME_L~1.TXT
```

> **Note:** If the output is the same as the input, either no short name exists, or the input was already a short name.

> **Tip:** You can also view all files and their short names (if they exist) in `cmd` with the command `dir /x`.

### Set the Short Name of a File

The command to modify the short name of a file is `python ShortName.py set [-q] FILE SHORTNAME`.

There are
[strict naming requirements](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-fscc/18e63b13-ba43-4f5f-a5b7-11e871b71f14)
on 8.3-style short names. Notably, they require:
- True ASCII only, in the 7-bit range
- No spaces
- 1-8 characters (other than `.`) before the extension
- *(Optional)* One `.` followed by 1-3 characters (other than `.`) for the extension

If a requested short name is invalid, ShortName will report an error that the name could not be set.

Example usage:

```cmd
python ShortName.py set .\some_long_file_name.txt short.txt
```

Example output:

```
Successfully set shortname of .\some_long_file_name.txt to "short.txt"
```

> **Note:** You can silence the success message with the `-q` or `--quiet` option.

## License

ShortName is free and open-source software provided under the [zlib license](https://opensource.org/licenses/Zlib).
