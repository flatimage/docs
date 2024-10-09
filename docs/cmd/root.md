# Execute a command as a regular user

## What is it?

`fim-root` executes a command as the root user inside the flatimage container.

## How to Use

You can use `./app.flatimage fim-help root` to get the following usage details:

```txt
Flatimage - Portable Linux Applications
fim-root:
   Executes a command as the root user
Usage:
   fim-root program-name [program-args...]
Example:
   fim-root bash
```

To install a program in the container:

```bash
# Allow network access
./app.flatimage fim-perms add network
# Install firefox
./app.flatimage fim-root pacman -S firefox
```

## How it Works

FlatImage uses [bubblewrap](https://github.com/containers/bubblewrap) to execute
commands inside a containerized environment, the programs are installed in an
overlay filesystem localized in the same folder as the current flatimage. If the
image is named `my-app`, the overlay filesystem is stored in `.my-app/overlays`
