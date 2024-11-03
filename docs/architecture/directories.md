# Directories

## Structure and Environment

The snippet below represents the structure of the flatimage temporary files
directory located in `/tmp/fim`, the corresponding environment variable is
shown between `[]`.

```
/tmp/fim [FIM_DIR_GLOBAL]
    ├── app
    │    └── app_id [FIM_DIR_APP]
    │        ├── bin [FIM_DIR_APP_BIN]
    │        └── instance
    │            └── instance_id [FIM_DIR_INSTANCE]
    │                └── mount [FIM_DIR_MOUNT]
    │                    ├── layers
    │                    │   ├── 0
    │                    │   ├── 1
    │                    │   ├── ...
    │                    │   └── n
    │                    └── overlayfs
    │
    └── run [FIM_DIR_RUNTIME]
        └── host [FIM_DIR_RUNTIME_HOST]
```

## The `app` Directory
- `/tmp/fim/app` is a directory containing data of flatimage applications,
each application has its own `id` that represents a specific build, for example,
`119216d_20241019145954` is a build of commit `119216d` from `2024-10-19` (YYYY-MM-DD)
built at `14h 59m 54s`.
- `/tmp/fim/app/app_id` is used to store `binaries` and create `instances` of
flatimage applications.
- `/tmp/fim/app/app_id/bin` contains static binaries for the current flatimage
build.
- `/tmp/fim/app/app_id/instance` contains instances of the current flatimage
build, these instances share the binaries located in `/tmp/fim/app/app_id/bin`.
- `/tmp/fim/app/app_id/instance/instance_id` contains the
read-only layer mountpoints and overlayfs mountpoint over all the layers
from `0` to `n`. The `id` for the `instance_id` directory is generated from a
call to `mkdtemp` with the template `XXXXXX`.

## The `run` Directory

The run directory contains `read-only` access to the host filesystem, it is only
accessible from inside the container and can be used to create symlinks for
libraries, sockets and more. This directory is used by the `gpu` permission to
symlink nvidia drivers.
