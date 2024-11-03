# Environment Variables

## What is it?
FlatImage provides a number of environment variables to query information about
directories, version, etc. These are separated in two groups, modifiable and
read-only:

**Modifiable**:

* `FIM_DEBUG`       : If defined to 1, print debug messages.
* `FIM_MAIN_OFFSET` : Shows filesystem offset and exits.

**Read-Only**:

* `FIM_VERSION`           : The version of the flatimage package
* `FIM_DIST`              : The linux distribution name (alpine, arch)
* `FIM_FILE_BINARY`       : Full path to the flatimage file
* `FIM_DIR_TEMP`          : Location of the runtime directory for instances of the current flatimage
* `FIM_DIR_MOUNT`         : Location of the runtime flatimage mountpoint
* `FIM_DIR_HOST_CONFIG`   : Configuration directory in the host machine

Furthermore, FlatImage also allows to the user to set the their own environment
variables.

## How to use

You can use `./app.flatimage fim-help env` to get the following usage details:

```
Flatimage - Portable Linux Applications
fim-env:
   Edit current permissions for the flatimage
Usage:
   fim-env add|set <'key=value'>...
   fim-env del <key>...
   fim-env list
Example:
   fim-env add 'APP_NAME=hello-world' 'PS1=my-app> ' 'HOME=$FIM_DIR_HOST_CONFIG/home'
```

The `env` command allows you to set new environment variables as so:

```bash
$ ./app.flatimage fim-env add 'MY_NAME=user' 'MY_STATE=sad'
```

To use these variables in the default boot command:

```bash
$ ./app.flatimage fim-boot sh -c 'echo "My name is $MY_NAME and I am $MY_STATE"'
$ ./app.flatimage
My name is user and I am sad
```

To list the set variables:
```bash
$ ./app.flatimage fim-env list
MY_NAME=user
MY_STATE=sad
```

To delete the set variables:
```bash
$ ./app.flatimage fim-env del MY_NAME MY_STATE
```

To enable debugging you can use:

```bash
$ FIM_DEBUG=1 ./app.flatimage
# or
$ export FIM_DEBUG=1
$ ./app.flatimage
```

## How it works

FlatImage defines environment variables during its boot process, they are used
to convey information about the directories to mount filesystems and query data.
