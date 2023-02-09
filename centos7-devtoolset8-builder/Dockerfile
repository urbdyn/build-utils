# This file builds an devtoolset-8 build image for Centos7

# Using CentOS 7 as base image to support building backwards compatible
# binaries with it.
# NOTE: CentOS 8 is EOL as of creating this file on 2023-02-09
FROM centos:7

# Installing tools needed for devtoolset-8 builds
RUN yum install -y which python3 centos-release-scl epel-release && \
    yum install -y ccache devtoolset-8 && \
    yum clean all && \
    rm /var/cache/yum/x86_64/7/timedhosts /var/cache/yum/x86_64/7/timedhosts.txt || true
