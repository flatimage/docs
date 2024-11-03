# Compression

## Setting the Compression Level

FlatImage compresses the changes in a novel layer with a compression level defined by
the variable `FIM_COMPRESSION_LEVEL`, which ranges between 0 and 10, the default
value is 7. To set a custom compression level export the variable before running
the `fim-commit` or `fim-layer` commands:

```
# To use half compression
export FIM_COMPRESSION_LEVEL=5
# To use full compression
export FIM_COMPRESSION_LEVEL=10
# To use minimum compression
export FIM_COMPRESSION_LEVEL=0
```
