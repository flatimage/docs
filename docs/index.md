<p align="center">
  <img src="https://raw.githubusercontent.com/flatimage/docs/master/docs/image/icon.png" width=150px/>
</p>

# FlatImage

## What is it?

FlatImage, is a hybrid of [Flatpak](https://github.com/flatpak/flatpak)
sandboxing with [AppImage](https://github.com/AppImage/AppImageKit) portability.

FlatImage use case is twofold:

* Flatimage is a package format, it includes a piece of software with all its
    dependencies for it work with across several linux distros (both Musl and
    GNU). Unlike `AppImage`, FlatImage runs the application in a container by
    default, which increases portability and compatibility at the cost of file
    size.

* Flatimage is a portable container image that requires no superuser permissions to run.

The diverse `GNU/Linux` ecosystem includes a vast array of distributions, each
with its own advantages and use cases. This can lead to cross-distribution
software compatibility challenges. FlatImage addresses these issues by:

* Utilizing its own root directory, enabling dynamic libraries with hard-coded
    paths to be packaged alongside the software without
    [binary patching](https://github.com/AppImage/AppImageKit/wiki/Bundling-Windows-applications).
* Running the application in its own gnu (or musl) environment, therefore, not using host
    libraries that might be outdated/incompatiblesystem with the application.

It simplifies the task of software packaging by enforcing the philosophy that it
should be as simple as setting up a container. This is an effort for the
end-user to not depend on the application developer to provide the portable
binary (or to handle how to package the application, dependencies and create a
runner script). It also increases the quality of life of the package developer,
simplifying the packaging process of applications.

## How to use

**Get FlatImage**

You can get the latest release [here](https://github.com/ruanformigoni/flatimage/releases), and extract the compressed archive with your file manager or with `tar -xf some-file.tar.xz`. To verify the image integrity, you can use the `sha256sum` file that accompanies each release, like so: `sha256sum -c some-file.flatimage.sha256sum`.

**Execute The Container**

You can enter the container simply by executing the downloaded image, e.g.,
`./app.flatimage`, which should give you a prompt like this `(flatimage@arch) →`.

To enter the container as root (to install software) use:
```
./app.flatimage fim-root bash
```

**Create a portable firefox installation**

TODO

## How it works

A FlatImage contains a container where it executes its own commands apart
from the host system. With that in mind, it is possible to create applications
to run in different linux systems (distributions) without worrying about missing
binaries or libraries.


# Motivations

1. The idea of this application sprung with the challenge to package software
   and dynamic libraries, such as `wine`, when there are hard-coded paths. The
   best solution is invasive
   [https://github.com/AppImage/AppImageKit/wiki/Bundling-Windows-applications](https://github.com/AppImage/AppImageKit/wiki/Bundling-Windows-applications)
   , which patches the binaries of wine directly to use a custom path for the
   32-bit libraries (an implementation of this concept is available
   [here](https://github.com/ruanformigoni/wine)), not only that, it requires to
   patch the `32-bit` pre-loader `ld-linux.so` as well, however, sometimes it
   still fails to execute properly. This is an over exceeding complexity for the
   end-user, which should package applications with no effort; `FlatImage`
   changes the root filesystem the application runs in, to a minimal gnu
   subsystem, and with that, it solves the previous issues with dynamic
   libraries no workarounds required. No host libraries are used, which
   decreases issues of portable applications working on one machine and not in
   other.

1. The fragmentation of the linux package management is considerable in modern
   times, e.g., `apt`, `pip`, `npm`, and more. To mitigate this issue
   `FlatImage` can perform the installation through the preferred package
   manager, and turn the program into an executable file, that can run in any
   linux distribution. E.g.: The user of `FlatImage` can create a binary of
   `youtube-dl`, from the `pip` package manager, without having either pip or
   python installed on the host operating system.

1. Some applications are offered as pre-compiled compressed tar files
   (tarballs), which sometimes only work when installed on the root of the
   operating system. However, doing so could hinder the operating system
   integrity, to avoid this issue `FlatImage` can install tarballs into itself
   and turn them into a portable binary.


# Related Projects

- [https://github.com/Kron4ek/Conty](https://github.com/Kron4ek/Conty)
- [https://github.com/genuinetools/binctr](https://github.com/genuinetools/binctr)
- [https://github.com/Intoli/exodus](https://github.com/Intoli/exodus)
- [https://statifier.sourceforge.net/](https://statifier.sourceforge.net/)
- [https://github.com/matthewbauer/nix-bundle](https://github.com/matthewbauer/nix-bundle)
- [https://github.com/containers/bubblewrap](https://github.com/containers/bubblewrap)
- [https://github.com/proot-me/proot](https://github.com/proot-me/proot)
