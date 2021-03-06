# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.68)
AC_INIT([liblouisutdml], [2.6.0], [liblouis-liblouisxml@freelists.org], [liblouisutdml], [http://www.liblouis.org])
AC_CONFIG_SRCDIR([liblouisutdml/semantics.c])
AC_CONFIG_HEADER([liblouisutdml/config.h])

AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE

# increment if the interface has additions, changes, removals.
LIBLOUISUTDML_CURRENT=7

# increment any time the source changes; set to
# 0 if you increment CURRENT
LIBLOUISUTDML_REVISION=0

# increment if any interfaces have been added; set to 0
# if any interfaces have been changed or removed. removal has
# precedence over adding, so set to 0 if both happened.
LIBLOUISUTDML_AGE=0

AC_SUBST(LIBLOUISUTDML_CURRENT)
AC_SUBST(LIBLOUISUTDML_REVISION)
AC_SUBST(LIBLOUISUTDML_AGE)

# Checks for programs.
AC_PROG_CC

# gnulib
gl_EARLY
gl_INIT

# Checks for more programs.
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
# AC_PROG_RANLIB
AC_ISC_POSIX
AC_LIBTOOL_WIN32_DLL
AM_PROG_LIBTOOL

# GNU help2man creates man pages from --help output; in many cases,
# this is sufficient, and obviates the need to maintain man pages
# separately. However, some developers do not have it so we do not
# make its use mandatory.
AC_CHECK_PROG([HELP2MAN], [help2man], [help2man])
AM_CONDITIONAL([HAVE_HELP2MAN], [test x$HELP2MAN = xhelp2man])

AC_PATH_PROG(PKG_CONFIG, pkg-config)

PKG_CHECK_MODULES(BASE_DEPENDENCIES, [liblouis >= 2.5.1, libxml-2.0])

# Checks for libraries.

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([stdlib.h string.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for library functions.
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_FUNC_STAT
AC_CHECK_FUNCS([memset])

case $host in
 *mingw* | *cygwin*)
 LDFLAGS="$LDFLAGS -avoid-version"
 CFLAGS="$CFLAGS -Wl,--add-stdcall-alias"
 ;;
esac

# Disable building the Java bindings on request
AC_ARG_ENABLE(
	[java_bindings], 
	[  --disable-java-bindings do not build the Java bindings],
	[case "${enableval}" in
	      yes) java_bindings=yes ;;
	      no)  java_bindings=no ;;
	      *) AC_MSG_ERROR([bad value ${enableval} for --disable-java-bindings]) ;;
	esac],[java_bindings=yes])
AM_CONDITIONAL([JAVA_BINDINGS], [test x$java_bindings == xyes])
AC_MSG_CHECKING([whether Java bindings should be built])
AC_MSG_RESULT($java_bindings)

if test x$java_bindings == xyes ; then

   # make sure jni include dirs are found
   # using a macro from the autoconf archive
   AX_JNI_INCLUDE_DIR

   for JNI_INCLUDE_DIR in $JNI_INCLUDE_DIRS
       do
           CPPFLAGS="$CPPFLAGS -I$JNI_INCLUDE_DIR"
	   found_jni_h=yes
       done
fi

if test x$java_bindings == xyes -a x$found_jni_h != xyes ; then
    AC_MSG_ERROR([Please install jni properly or disable the Java bindings with --disable-java-bindings.])
fi

AC_CONFIG_FILES([Makefile
	gnulib/Makefile
	doc/Makefile
	java/Makefile
	java/lib/Makefile
	java/src/Makefile
	java/src/org/Makefile
	java/src/org/liblouis/Makefile
	java/tests/Makefile
	java/tests/org/Makefile
	java/tests/org/liblouis/Makefile
	java/testdata/Makefile
	java/testdata/liblouis/Makefile
	java/testdata/liblouis/tables/Makefile
	java/testdata/liblouisutdml/Makefile
	java/testdata/liblouisutdml/lbu_files/Makefile
	man/Makefile
	lbu_files/Makefile
	liblouisutdml/Makefile
	liblouisutdml.pc
	tests/Makefile
	tests/test_suite/Makefile
	tests/test_suite/test_01/Makefile
	tests/test_suite/test_02/Makefile
	tests/test_suite/test_03/Makefile
	tests/test_suite/test_04/Makefile
	tests/test_suite/test_05/Makefile
	tests/test_suite/test_06/Makefile
	tests/test_suite/test_07/Makefile
	tests/test_suite/test_08/Makefile
	tests/test_suite/test_09/Makefile
	tests/test_suite/test_10/Makefile
	tests/test_suite/test_11/Makefile
	tests/test_suite/test_12/Makefile
	tests/test_suite/test_13/Makefile
	tests/test_suite/test_14/Makefile
	tools/Makefile
	windows/Makefile
	windows/include/Makefile
	m4/Makefile])

AC_OUTPUT

