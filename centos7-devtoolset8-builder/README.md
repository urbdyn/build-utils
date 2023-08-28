# urbdyn/centos7-devtoolset8-builder

This is a Docker container for building binaries on Centos7 using the `devtoolset-8` toolchain bundle.

It has the benefit of providing all the needed boiler plate and avoiding the long waits in CI needed to install the full build `devtoolset-8`  toolchain in a clean container.
Also, `devtoolset-8` allows for building binaries which are backwards compatible with Centos7 while still have newer build dependencies as available in Centos / Rocky Linux 8.

Our recommended use of it is to build your own container with it to ensure you have any other dependencies you need.
To use to build something 

## Creating container with this container

```Dockerfile
FROM urbdyn/centos7-devtoolset8-builder:latest

# Install any needed packages here
# ...
```

## Running container

```bash
docker create -it \
    --name "$container_builder_container" \
    -v "$build_dir/:/TARGET_BUILD_DIR_HERE/" \
    "$container_builder_image"
```

## Change Log

### 2023-02-09 (commit `08028c2`)

Commit: https://github.com/urbdyn/build-utils/commit/08028c28122b706e230841b770fa62180b3b11e7

Container: https://github.com/urbdyn/build-utils/pkgs/container/centos7-devtoolset8-builder/69516047


Changes:
1. First release of container.
