# Execute a command as a regular user

## What is it?

`fim-exec` executes a command as a regular user inside the flatimage container,
if the `HOME` permission is set, it also allows access to the host home
directory.

## How to Use

You can use `./app.flatimage fim-help exec` to get the following usage details:

```txt
Flatimage - Portable Linux Applications
fim-exec:
   Executes a command as a regular user
Usage:
   fim-exec program-name [program-args...]
Example:
   fim-exec bash
```

To run a program installed in the container:

```bash
./app.flatimage fim-exec firefox
```

## How it Works

If the image is named `my-app`, the program data is stored in an overlay
filesystem in `.my-app/overlays`.
