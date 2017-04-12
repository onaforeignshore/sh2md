# sh2md - Shell script comment to Markdown converter

Converts comments to Markdown that may be used in reference documentation.

## Usage

`sh2md` has no args and expects a shell script with comments as described below on the stdin and will markdown output result on the stdout.

To display shell script Markdown on screen:
```sh
$ ./sh2md sample.sh
```

To redirect shell script Markdown to a file:
```sh
$ ./sh2md sample.sh > sample.md
```

You can also use pipe redirection:
```sh
$ cat sample.sh | sh2md
```


## Fields

### File description block
| Field         | Type         | Description                 |
|---------------|:------------:|-----------------------------|
| `@title`      | single       | The file's title            |
| `@info`       | multi        | Information about the file  |
| `@version`    | single       | Version information         |
| `@author`     | single/multi | File authors                |
| `@dependency` | single/multi | Any dependencies            |

### Function block
| Field           | Type         | Description                               |
|-----------------|:------------:|-------------------------------------------|
| `@description`  | multi        | Function description                      |
| `@example`      | single/multi | Usage example                             |
| `@arg`/`@param` | single/multi | Arguments                                 |
| `@noarg`        | _None_       | Field that returns "_Function has no arguments._" |
| `@var`          | single/multi | Variables                                 |
| `@return`       | single/multi | Returns                                   |
| `@exitcodes`    | single/multi | Exit codes                                |
| `@see`          | single/multi | Reference to another function in the file |
| `@stdout`       | single/multi | Standard output                           |

#### Please note

`single/multi` fields also accept plural forms, eg. `@authors`, `@dependencies`, etc.

For `multi` fields (`@info` and `@description`), you should use `##` to indicate the end of the field (to avoid issues with multiple empty lines). The field will be converted into paragraphs and extra newlines will be removed.

## TODO

- [ ] Add more fields.

## Example

`sh2md` will match comments at the top of the file...

```sh
######################################################################
# @title sh2md - Bash comment to Markdown converter
#
# @info
# sh2md is based on [shdoc](https://github.com/reconquest/shdoc), but has been rewritten from scratch with many improvements.
##
# @author
#   [onaforeignshore](https://github.com/onaforeignshore)
#
# @dependencies gawk
#
# @source https://github.com/onaforeignshore/sh2md
##
```

...and before function definitions

```sh
# @description Multiline description goes here and
# there
##
# @example
#   someFunc a b c
#   echo 123
#
# @arg $1 string Some arg.
# @arg $@ any Rest of arguments.
#
# @noargs
#
# @exitcode 0  If successfull.
# @exitcode >0 On failure
# @exitcode 5  On some error.
#
# @stdout Path to something.
#
# @see anotherFunc()
someFunc() {
```

To produce following output

---

# sh2md - Shell script comment to Markdown converter

### File Description

_sh2md is based on [shdoc](https://github.com/reconquest/shdoc), but has been rewritten from scratch with many improvements._

### Author(s)

- [onaforeignshore](https://github.com/onaforeignshore)

### Dependencies

- gawk

### Source(s)

[https://github.com/onaforeignshore/sh2md](#https://github.com/onaforeignshore/sh2md)

## Table of Contents

- [someFunc()](#someFunc)

## someFunc()
Multiline description goes here and
there

### Example

```bash
someFunc a b c
echo 123
```

### Arguments

- **$1** (string) Some arg.
- **...** (any) Rest of arguments.
- _Function has no arguments._

### Exit codes

- **0**  If successfull.
- **>0** On failure
- **5**  On some error.

### Output on stdout

- Path to something.

### See also

- [anotherFunc()](#anotherFunc())

---

