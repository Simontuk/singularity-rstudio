BootStrap: shub
From: Simontuk/singularity-r

%labels
  Maintainer Simon Steiger
  RStudio_Version 1.2.1335

%help
  This will run RStudio Server

%apprun rserver
  exec rserver "${@}"

%runscript
  exec rserver "${@}"

%environment
  export PATH=/usr/lib/rstudio-server/bin:${PATH}

%setup
  install -Dv \
    rstudio_auth.sh \
    ${SINGULARITY_ROOTFS}/usr/lib/rstudio-server/bin/rstudio_auth
  install -Dv \
    ldap_auth.py \
    ${SINGULARITY_ROOTFS}/usr/lib/rstudio-server/bin/ldap_auth

%post
  # Software versions
  export RSTUDIO_VERSION=1.2.1335

  # Install RStudio Server
  yum update
  yum install -y \
    ca-certificates \
    wget

  wget --no-verbose \
    -O rstudio-server.rpm \
    https://download2.rstudio.org/server/centos6/x86_64/rstudio-server-rhel-${RSTUDIO_VERSION}-x86_64.rpm
  yum install -y rstudio-server.rpm
  rm -f rstudio-server.rpm

  # Add support for LDAP authentication
  yum -y install https://centos7.iuscommunity.org/ius-release.rpm
  yum -y install python36u
  yum -y install python36u-pip
  pip3.6 install ldap3

  #htop
  yum install -y htop ksh
  # Clean up
  yum clean all
