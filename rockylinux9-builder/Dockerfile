# This file builds an build image for Rocky Linux 9

# Using Rocky Linux 9.5 as base image (pulled on date 2025-03-03).
FROM docker.io/rockylinux/rockylinux@sha256:149fd31d916038eb1084d0e051537e279d7afcd5de0b365254e8fa3c3ef12bad

# Installing tools needed for builds
RUN dnf install -y which python3 epel-release && \
    dnf groupinstall -y "Development Tools" && \
    dnf install -y ccache && \
    dnf clean all
