# Limelight - DB Processor [![master](https://github.com/limelight-development/db-processor/workflows/CI%20Test/badge.svg)](https://github.com/limelight-development/db-processor/actions?query=workflow%3A%22CI+Test%22)


```
#================================================================
# Limelight - DB Processor
#================================================================
# SYNOPSIS
#   ./db-processor
#   ./db-processor [[input-maps]INPUT_MAPS] ...
#
# DESCRIPTION
#    This script is used to process INSERT statements
#    based on key-value maps into a database.
#    
#    Processing includes escaping the values (prepared-statements).
#
#    The script incorporates arguments and env variables.
#    If no arguments are provided, you must export the required
#    environment variables prior to running it.
#
# ARGUMENTS
#       [[input-maps]INPUT_MAPS]    Set the key-value map
#                                   The default value is env INPUT_MAPS
#                                   Format: String
#       [[input-host]INPUT_HOST]    Set the mysql host
#                                   The default value is env INPUT_HOST
#                                   Format: String|IP
#       [[input-port]INPUT_PORT]    Set the mysql port
#                                   The default value is env INPUT_PORT
#                                   Format: String|Integer
#       [[input-user]INPUT_USER]    Set the mysql username
#                                   The default value is env INPUT_USER
#                                   Format: String
#       [[input-pass]INPUT_PASS]    Set the mysql password
#                                   The default value is env INPUT_PASS
#                                   Format: String
#       [[input-tabl]INPUT_TABL]    Set the mysql table, eg: db.tbl
#                                   The default value is env INPUT_TABL
#                                   Format: String
#       [[input-debug]INPUT_DEBUG]  Toggle the debug mode
#                                   The default value is env INPUT_DEBUG
#                                   or false
#                                   Format: Boolean/Integer
#
# EXAMPLES
#    ./db-processor "column1=value1;column2=value2" ...
#
#================================================================
#- IMPLEMENTATION
#-    version         1.0.0
#-    author          Steven Agyekum <s-8@posteo.mx>
#-    copyright       Copyright (c) Limelight Gaming Ltd.
#-    license         MIT License
#-
#================================================================
#================================================================
```
---

## Use Case

We use this product in our CD workflows for tracking some commit messages.

## Usage

### Standalone

Requirements:

- MySQL client
- PHP 7 with PDO extension enabled

Permissions:

``chmod +x ./db-processor``

Execution:

```
./db-processor <args>
```

or 

```
./db-processor
``` 

when using environment variables.

### Docker

Build the container using the Dockerfile and run:

```
docker run -e INPUT_MAPS="" -e INPUT_HOST="" -e INPUT_PORT="" -e INPUT_USER="" -e INPUT_PASS="" -e INPUT_TABL="" -e INPUT_DEBUG=true
```

### Github Actions

You can run this action by using the ``with:`` block

```
  steps:
  - uses: actions/checkout@v2
  - name: Insert to database
    uses: limelight-development/db-processor@2.0
    with:
      maps: column1=value1;column2=value2;
      host: ${{ secrets.MYSQL_HOST }}
      port: ${{ secrets.MYSQL_PORT }}
      user: ${{ secrets.MYSQL_USER }}
      pass: ${{ secrets.MYSQL_PASS }}
      tabl: ${{ secrets.MYSQL_TABL }}
      debug: true
```

or by using the ``env:`` block for environment variables

```
  steps:
  - uses: actions/checkout@v2
  - name: Insert to database
    uses: limelight-development/db-processor@2.0
    env:
      INPUT_MAPS: column1=value1;column2=value2;
      INPUT_HOST: ${{ secrets.MYSQL_HOST }}
      INPUT_PORT: ${{ secrets.MYSQL_PORT }}
      INPUT_USER: ${{ secrets.MYSQL_USER }}
      INPUT_PASS: ${{ secrets.MYSQL_PASS }}
      INPUT_TABL: ${{ secrets.MYSQL_TABL }}
      INPUT_DEBUG: true
```

**Full example:**

```
name: CI

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Insert to database
      uses: limelight-development/db-processor@2.0
      with:
        maps: column1=value1;column2=value2;
        host: ${{ secrets.MYSQL_HOST }}
        port: ${{ secrets.MYSQL_PORT }}
        user: ${{ secrets.MYSQL_USER }}
        pass: ${{ secrets.MYSQL_PASS }}
        tabl: ${{ secrets.MYSQL_TABL }}
        debug: true

```
---

Check synopsis above to get an example.

## Demo

Check the Actions tab for a live demo:

[Live Demo](https://github.com/limelight-development/db-processor/commit/9a8572f50193c5f9c624dc7772600cd629bd01c6/checks?check_suite_id=344054328)

## Debug Output

[![debug](https://i.imgur.com/IYt9zKF.png)]

