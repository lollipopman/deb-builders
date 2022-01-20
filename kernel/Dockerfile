ARG CODENAME
FROM debian:${CODENAME}
ARG CODENAME

RUN echo "deb http://deb.debian.org/debian ${CODENAME}-backports main" > /etc/apt/sources.list.d/backports.list
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    bc \
    bison \
    build-essential \
    ca-certificates \
    curl \
    dwarves \
    fakeroot \
    flex \
    initramfs-tools \
    libelf-dev \
    libelf1 \
    libperl-dev \
    libssl-dev \
    lsb-release \
    rsync \
    xz-utils \ 
    2>&1

# needed by debian kernel config, copied from upstream source pkg
COPY debian-uefi-certs.pem /
COPY make-deb /usr/local/bin/
RUN chmod 555 /usr/local/bin/make-deb

CMD make-deb
