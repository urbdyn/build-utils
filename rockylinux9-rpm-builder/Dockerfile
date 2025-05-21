# This file builds an RPM build image for Rocky Linux 9

# Using Rock Linux 9 as base image to support rpmbuild
FROM rockylinux:9

# Installing tools needed for rpmbuild
RUN dnf install -y rpm-build rpmlint rpmdevtools systemd sudo selinux-policy-devel && \
    dnf clean all

# Copy over helper scripts
COPY setup_rpm_users /usr/bin/setup_rpm_users
COPY build_rpm_from_env_vars /usr/bin/build_rpm_from_env_vars

# Setup commend to run by default
CMD build_rpm_from_env_vars run
