# Commit current changes to the FlatImage

## What is it?

`fim-commit` is a command to integrate the current changes with the FlatImage.

## How to Use

```bash
# Allow network access
./app.flatimage fim-perms add network
# Install firefox
./app.flatimage fim-root pacman -S firefox
# Compress firefox and its dependencies into a new layer, and include it in the flatimage
./app.flatimage fim-commit
```

## How it Works

`fim-commit` compresses the modified and/or newly created files from the
`overlay filesystem` into a new layer; afterwards, it includes this layer in the
top of the layer stack of the current image.

<p align="center">
  <img src="/image/commit.png"/>
</p>
