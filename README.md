# Static builds of `clangd` and `clang-format`

These builds are fully done with github-actions.

Versions for Linux ARM are also available, cross-compiled from the Linux host.

## Download

The latest available builds are [here](https://github.com/arduino/clang-static-binaries/releases/latest).
Go to the [releases page](https://github.com/arduino/clang-static-binaries/releases) for all the available versions.

## Archive contents

`clang-format_<version>_<platform>.tar.bz2` contains a single executable:

```
clang_<platform>/clang-format[.exe]
```

`clangd_<version>_<platform>.tar.bz2` additionally ships clangd's resource directory, which
holds its builtin headers (`stddef.h`, `stdint.h`, `float.h`, the `__stddef_*` family, the
target intrinsics headers, ...):

```
clang_<platform>/clangd[.exe]
clang_<platform>/clang-resource/include/...
```

**Extract the whole `clang_<platform>/` tree.** clangd looks for its resource directory next
to its own executable, so `clang-resource` must stay a sibling of the binary. Without it,
clangd 21 and later report builtin headers as missing whenever a `--query-driver`
cross-compilation toolchain is in use — silently masked by the host SDK on macOS and Linux,
but broken outright on Windows.
