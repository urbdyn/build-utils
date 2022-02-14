# urbdyn/centos7-rpm-builder

This is a Docker container for building Centos7 RPM packages.

It has the benefit of providing all the needed boiler plate and avoiding the long waits in CI needed to install the full build toolchain in a clean container.

Our recommended use of it is to build your own container with it to ensure the user/group of the person running the container matches that of the internal container user.
This means you can easily copy files and mount directories between the host and container without issue.

```Dockerfile
FROM urbdyn/centos7-rpm-builder:latest

# Accept user input when building container with fallback to common Linux user pattern
ARG _USER_ID
ARG _GROUP_ID
ENV _USER_ID ${_USER_ID:-1001}
ENV _GROUP_ID ${_GROUP_ID:-1002}

# Run script to create users and declare new user as default
RUN setup_users.sh
USER $_USER_ID:$_GROUP_ID

# Install any needed packages here
# ...
```
