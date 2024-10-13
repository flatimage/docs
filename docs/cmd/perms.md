# Configure permissions

## What is it?

It is a functionally to allow granular access to the host's resources.

## How to use

You can use `./app.flatimage fim-help perms` to get the following usage details:

```txt
fim-perms : Edit current permissions for the flatimage
Commands:
   add,del,list,
   add : Allow one or more permissions
   del : Delete one or more permissions
   list : List current permissions
Note: Permissions: home,media,audio,wayland,xorg,dbus_user,dbus_system,udev,usb,input,gpu,network
Usage: fim-perms add <perms...>
   <perms> : One or more permissions
Usage: fim-perms del <perms...>
   <perms> : One or more permissions
Usage: fim-perms list
Example: fim-perms add home,network,gpu
```

---

To allow the access to a resource, use the `add` subcommand:

```
$ ./app.flatimage fim-perms add home
```

This will make the `home` directory of the host accessible from the container.

---

To reset all permissions to a specific list of permissions, use `set`:

```
$ ./app.flatimage fim-perms set media,audio,wayland,xorg,dbus_user,dbus_system,udev,usb,input,gpu,network
```

This will allow access to the majority of resources, except `home`.

---

To list the current permissions, use `list`:

```
$ ./app.flatimage fim-perms list
```

This will list all the **currently set** permissions.

---

## How it works

FlatImage uses [bubblewrap's](https://github.com/containers/bubblewrap)
bind mechanisms to make devices and directories available in the guest
container.
