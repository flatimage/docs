# Bind Host Paths

## What is it?

This is a mechanism to make specific paths from the host available inside the guest container.

## How to use

You can use `./app.flatimage fim-help env` to get the following usage details:

```txt
fim-bind : Bind paths from the host to inside the container
Commands:
   add,del,list,
   add : Create a novel binding of type <type> from <src> to <dst>
   del : Deletes a binding with the specified index
   list : List current bindings
Usage: fim-bind add <type> <src> <dst>
   <type> : ro, rw, dev
   <src> : A file, directory, or device
   <dst> : A file, directory, or device
Usage: fim-bind del <index>
   <index> : Index of the binding to erase
Usage: fim-bind list
```

---

To bind a device from the host to use in the guest:
```
./app.flatimage fim-bind add dev /dev/my_device /dev/my_device
```
This will make `my_device` available inside the container.

---

To bind a file path from the host to the guest as read-only:
```
./app.flatimage fim-bind add ro /home/my-user/Music /Music
```
This will make the `Music` directory available inside the container in `/Music`,
as read-only.

---

To bind a file path from the host to the guest as read-write:
```
./app.flatimage fim-bind add rw /home/my-user/Music /Music
```
This will make the `Music` directory available inside the container in `/Music`,
as read-write.

## How it works

FlatImage uses [bubblewrap's](https://github.com/containers/bubblewrap)
bind mechanisms to make devices and directories available in the guest
container.
