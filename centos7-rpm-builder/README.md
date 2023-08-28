# urbdyn/centos7-rpm-builder

This is a Docker container for building Centos7 RPM packages.

It has the benefit of providing all the needed boiler plate and avoiding the long waits in CI needed to install the full build toolchain in a clean container.

Our recommended use of it is to build your own container with it to ensure the user/group of the person running the container matches that of the internal container user.
This means you can easily copy files and mount directories between the host and container without issue.

## Creating container with this container

```Dockerfile
FROM urbdyn/centos7-rpm-builder:latest

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

### 2023-08-28 (commit `a5fff7e`)

Commit: https://github.com/urbdyn/build-utils/commit/a5fff7e71fedb73ff46a1f2a29dfb8ffc69ed56f

Container: https://github.com/urbdyn/build-utils/pkgs/container/centos7-rpm-builder/122657794

Changes:
1. Updated `setup_rpm_users` script to support if an existing user ID or group ID is given.


### 2022-02-14.3 (commit `11d5170`)

Commit: https://github.com/urbdyn/build-utils/commit/11d51707a1b8284dbc0e874e6c6038657c556fb5

Container: https://github.com/urbdyn/build-utils/pkgs/container/centos7-rpm-builder/15029728

Changes:
1. Added cleanup to package install to reduce container size.


### 2022-02-14.2 (commit `afa0152`)

Commit: https://github.com/urbdyn/build-utils/commit/afa0152158ea3aab45f9a387e91e49ff4e4ffe57

Container: https://github.com/urbdyn/build-utils/pkgs/container/centos7-rpm-builder/15026138

Changes:
1. Added support for building multiple packages.


### 2022-02-14.1 (commit `3600f92`)

Commit: https://github.com/urbdyn/build-utils/commit/3600f924b4ce6cb6919003b5cf7645d4f3b0c8ed

Container: https://github.com/urbdyn/build-utils/pkgs/container/centos7-rpm-builder/15025045

Changes:
1. First release of container.
