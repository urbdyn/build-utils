# urbdyn/rockylinux9-rpm-builder

This is a Docker container for building Rocky Linux 9 RPM packages.

It has the benefit of providing all the needed boiler plate and avoiding the long waits in CI needed to install the full build toolchain in a clean container.

Our recommended use of it is to build your own container with it to ensure the user/group of the person running the container matches that of the internal container user.
This means you can easily copy files and mount directories between the host and container without issue.

## Creating container with this container

```Dockerfile
FROM urbdyn/rockylinux9-rpm-builder:latest

# Accept user input when building container with fallback to common Linux user pattern
ARG _USER_ID
ARG _GROUP_ID
ENV _USER_ID ${_USER_ID:-1001}
ENV _GROUP_ID ${_GROUP_ID:-1002}

# Run script to create users and declare new user as default
RUN setup_rpm_users
USER $_USER_ID:$_GROUP_ID

# Install any needed packages here
# ...
```

## Running container

```bash
docker create -it \
    --user "$_uid:$_gid" \
    --name "$container_builder_container" \
    -v "$build_dir/:/home/builder/rpmbuild/" \
    -e SPEC_FILE_NAMES="foobar.spec" \
    -e PACKAGE_NAME="foobar" \
    -e PACKAGE_VERSION="1.2.3" \
    -e PACKAGE_LICENSE="MY LICENSE" \
    -e PACKAGE_SOURCE="foobar.tar.gz" \
    "$container_builder_image"
```


## Change Log

### 2025-05-21 (commit `b526629`)

Commit: https://github.com/urbdyn/build-utils/commit/b526629c4e9ccb2dea48ca0850df1957adfebd9d

Container: https://github.com/urbdyn/build-utils/pkgs/container/rockylinux9-rpm-builder/421008777

Changes:
1. First release of container.
