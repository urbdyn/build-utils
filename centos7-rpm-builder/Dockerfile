# This file builds an RPM build image for Centos7

# Using CentOS 7 as base image to support rpmbuild
# NOTE: CentOS 8 is EOL as of creating this file on 2022-02-14
FROM centos:7

# Installing tools needed for rpmbuild
RUN yum install -y rpm-build rpmlint rpmdevtools systemd sudo selinux-policy-devel && \
    yum clean all && \
    rm /var/cache/yum/x86_64/7/timedhosts /var/cache/yum/x86_64/7/timedhosts.txt || true

# Copy over helper scripts
COPY setup_rpm_users /usr/bin/setup_rpm_users
COPY build_rpm_from_env_vars /usr/bin/build_rpm_from_env_vars

# Setup commend to run by default
CMD build_rpm_from_env_vars run
