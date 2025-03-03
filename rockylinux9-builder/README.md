# urbdyn/rockylinux9-builder

This is a Docker container for building binaries on Rocky Linux 9 using the standard `"Development Tools"` group install.

It has the benefit of providing all the needed boiler plate and avoiding the long waits in CI needed to install the full build `"Development Tools"` toolchain in a clean container.

Our recommended use of it is to build your own container with it to ensure you have any other dependencies you need.
To use to build something follow the below sections:

## Creating container with this container

```Dockerfile
FROM urbdyn/rockylinux9-builder:latest

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
