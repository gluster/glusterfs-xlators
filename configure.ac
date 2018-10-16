dnl Copyright 2018 Red Hat, Inc.

AC_PREREQ([2.69])

AC_INIT([glusterfs-posix2], [1.0], [bugmenot@gluster.org])

AC_SUBST([PACKAGE_RELEASE], 1)

AM_INIT_AUTOMAKE(tar-pax)

AC_CONFIG_HEADER([config.h])

AC_CONFIG_FILES([glusterfs-posix2.spec
                 Makefile
                 xlators/Makefile
                 xlators/experimental/Makefile
                 xlators/experimental/posix2/Makefile
                 xlators/experimental/posix2/common/Makefile
                 xlators/experimental/posix2/common/src/Makefile
                 xlators/experimental/posix2/ds/Makefile
                 xlators/experimental/posix2/ds/src/Makefile
                 xlators/experimental/posix2/mds/Makefile
                 xlators/experimental/posix2/mds/src/Makefile
                ])

AM_MAINTAINER_MODE

AC_DEFINE([COPYRIGHT], ["Copyright (C) 2018 Red Hat, Inc."], [Copyright notice])

# Checks
AC_PROG_CC
AC_DISABLE_STATIC
AC_PROG_LIBTOOL

# Dependencies
dnl Because there isn't a pkg-conf for glusterfs-devel
PKG_CHECK_MODULES([GFAPI], [glusterfs-api >= 3.12.0],,[AC_MSG_ERROR([cannot find glusterfs api headers])])
PKG_CHECK_MODULES([UUID], [uuid],, [AC_MSG_ERROR([cannot find libuuid headers])])

case $host_os in
     *netbsd*)
        GF_HOST_OS="GF_BSD_HOST_OS"
        ;;
     *freebsd*)
        GF_HOST_OS="GF_BSD_HOST_OS"
        ;;
     darwin*)
        GF_HOST_OS="GF_DARWIN_HOST_OS"
        ;;
     *)
        GF_HOST_OS="GF_LINUX_HOST_OS"
        ;;
esac

dnl
dnl Word sizes...
dnl
AC_CHECK_SIZEOF(short)
AC_CHECK_SIZEOF(int)
AC_CHECK_SIZEOF(long)
AC_CHECK_SIZEOF(long long)
SIZEOF_SHORT=$ac_cv_sizeof_short
SIZEOF_INT=$ac_cv_sizeof_int
SIZEOF_LONG=$ac_cv_sizeof_long
SIZEOF_LONG_LONG=$ac_cv_sizeof_long_long
AC_SUBST(SIZEOF_SHORT)
AC_SUBST(SIZEOF_INT)
AC_SUBST(SIZEOF_LONG)
AC_SUBST(SIZEOF_LONG_LONG)

GF_CPPINCLUDES='-include $(top_builddir)/config.h'
GF_CPPDEFINES="-D_GNU_SOURCE -D${GF_HOST_OS}"
GF_CPPFLAGS="$GF_CPPDEFINES $GF_CPPINCLUDES"
AC_SUBST(GF_CPPFLAGS)
GF_CFLAGS="-I/usr/include/glusterfs -I/usr/include/glusterfs/rpc -I/usr/include/glusterfs/xdr -isystem /usr/include/tirpc ${GFAPI_CFLAGS}"
AC_SUBST(GF_CFLAGS)
GF_LIBS="$(echo ${GFAPI_LIBS} | sed -e 's/ -lgfapi//')"
AC_SUBST(GF_LIBS)
HAVE_ATOMIC_BUILTINS="yes"
AC_SUBST(HAVE_ATOMIC_BUILTINS)

dnl gfapi Version: is the "api version" but we can infer which
dnl version of glusterfs it is.
PACKAGE_VERSION=$(pkg-config --modversion glusterfs-api | sed -e 's/[0-9]\.//')
AC_SUBST(PACKAGE_VERSION)
VERSION=${PACKAGE_VERSION}
AC_SUBST(VERSION)

AC_OUTPUT

cat <<EOF

------------------ Summary ------------------
 $PACKAGE_NAME version $PACKAGE_VERSION
  Prefix.........: $prefix
  C Compiler.....: $CC $CFLAGS $CPPFLAGS
  Linker.........: $LD $MORE_LDFLAGS $LDFLAGS $LIBS
---------------------------------------------

Check the above options and compile with:
 ${MAKE-make}

EOF
