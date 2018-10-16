
SUBDIRS = xlators

EXTRA_DIST = autogen.sh glusterfs-posix2.spec \
	AUTHORS  autogen.sh  ChangeLog  configure.ac  COPYING-GPLV2 COPYING-LGPLV3 \
	INSTALL  NEWS  README

gitclean: clean distclean
	find . -path gnulib -prune -name Makefile.in -exec rm -f {} \;
	find . -path gnulib -prune -name Makefile -exec rm -f {} \;
	rm -f aclocal.m4 compile config.* configure depcomp install-sh libtool \
		ltmain.sh missing stamp-h1
	rm -rf autom4te.cache
