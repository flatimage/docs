# Bind Host Paths

## What is it?

It specifies the default command to execute when no arguments are passed for the FlatImage.

## How to use

You can use `./app.flatimage fim-help boot` to get the following usage details:

```txt
fim-boot : Configure the default startup command
Commands:
   boot,
   boot : Execute <command> with optional [args] when FlatImage is launched
Usage: fim-boot <command> [args...]
   <command> : Startup command
   <args> : Arguments for the startup command
Example: fim-boot echo test
Note: To restore the default behavior use `fim-boot bash`
```

---

To change the default command to echo:

```bash
$ ./app.flatimage fim-boot echo
```

Now FlatImage will call echo by default:

```bash
$ ./app.flatimage hello world
hello world
```

You can also provide extra arguments to the command, these will always be prepended to the following arguments:

```bash
$ ./app.flatimage fim-boot echo "PREFIX: "
$ ./app.flatimage fim-boot hello world
PREFIX: hello world
```


## How it works

The command is written to the `boot.json` file in the `/fim/config` directory. FlatImage checks this file before starting looking for a default command and arguments. If this file is missing or corrupted, FlatImage falls back to bash.