# shards-lang boost dependencies

This repository contains build scripts to bundle the boost sources required to build [shards](https://github.com/fragcolor-xyz/shards)

We emphasize libraries that work well with the C++ Standard Library. Boost
libraries are intended to be widely useful, and usable across a broad spectrum
of applications. The Boost license encourages both commercial and non-commercial use
and does not require attribution for binary use.

The packaged sources are fetched from a github release in this repository using:

```cmake
FetchContent_Declare(
    boost
    URL      https://github.com/shards-lang/boost/releases/download/boost-f74a225c09-2/output.7z
    URL_HASH SHA256=7C876AC31F7D1A80C9B4671FD960399F86CF24DC9DA83AFF7F1CBC8984424080
)
```

## Packaging a new version

When a tag is pushed to this repository, the CI step will run the `package_shards` script and make a release linked to that tag, reference the new archive URL and hash in the original project.

## Adding dependencies

Add dependencies to the array `MODULES` inside the `package_shards` script

## Updating

To update this repository use a `git rebase -i <commit>`, where `<commit>` is probably a tagged release commit from the [upstream superproject](https://github.com/boostorg/boost) (e.g. `boost-1.81.0`)

Make sure to include the commits containing this doc and package script on top of the rebase, alongside and submodule modifications. To keep it easy to update, you should tag shards specific commits with `[shards]`

NOTE: Any newly added submodules by boost should be modified to reference the absolute url, e.g. `https://github.com/boostorg/url.git` instead of `../url.git`


## Building boostdep

just run `cmake -Bbuild_tools tools/boostdep` then `cmake --build build_tools --target boostdep --config Release`

Update BOOSTDEP to point to the binary
