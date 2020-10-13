dnl#                                               -*- Autoconf -*-
dnl# Process this file with autoconf to produce a configure script.

AC_INIT([xfsdump],[3.0.6],[])
AC_CONFIG_SRCDIR([common/main.c])
AC_PREREQ([2.69.185-b502e])
AC_CONFIG_AUX_DIR([.])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_HEADER([include/config.h])
AC_PREFIX_DEFAULT([/usr])

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MAKE_SET

LT_INIT

# flags that can be passed to this configure script:
AC_ARG_ENABLE([shared],
[AS_HELP_STRING([--enable-shared=[yes/no]],
                [Enable use of shared libraries [default=yes]])],[],
	[enable_shared=yes])
AC_SUBST([enable_shared])dnl

AC_ARG_ENABLE([gettext],
[AS_HELP_STRING([--enable-gettext=[yes/no]],
                [Enable alternate language support [default=yes]])],[],
	[enable_gettext=yes])
AC_SUBST([enable_gettext])dnl

AC_ARG_ENABLE([lib64],
[AS_HELP_STRING([--enable-lib64=[yes/no]],
                [Enable lib64 support [default=yes]])],[],
	[enable_lib64=yes])
AC_SUBST([enable_lib64])dnl

#
# If the user specified a libdir ending in lib64 do not append another
# 64 to the library names.
#
base_libdir=`basename "$libdir"`
case ${base_libdir} in
lib64)
  enable_lib64=no
esac

#
# Some important tools should be installed into the root partitions.
#
# Check whether exec_prefix=/usr: and install them to /sbin in that
# case.  If the user choses a different prefix assume he just wants
# a local install for testing and not a system install.
#
case ${exec_prefix}:${prefix} in
NONE:NONE | NONE:/usr | /usr:*)
  root_sbindir='/sbin'
  root_libdir="/${base_libdir}"
  ;;
*)
  root_sbindir="${sbindir}"
  root_libdir="${libdir}"
  ;;
esac

AC_SUBST([root_sbindir])dnl
AC_SUBST([root_libdir])dnl

# Find localized files
LOCALIZED_FILES=""
for lfile in `find ${srcdir} -name '*.c' -type f || exit 1`; do
    LOCALIZED_FILES="${LOCALIZED_FILES} \$(TOPDIR)/$lfile"
done
AC_SUBST([LOCALIZED_FILES])dnl

# Checks for header files.
AC_HEADER_MAJOR
AC_CHECK_HEADERS([fcntl.h malloc.h malloc/malloc.h mntent.h stdint.h stdio.h \
                  sys/file.h sys/ioctl.h sys/param.h sys/socket.h \
                  sys/statvfs.h termios.h unistd.h utime.h])dnl

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_UID_T
AC_C_INLINE
AC_TYPE_INT32_T
AC_TYPE_INT64_T
AC_TYPE_MODE_T
AC_TYPE_OFF_T
AC_TYPE_PID_T
AC_TYPE_SIZE_T
AC_TYPE_SSIZE_T
AC_CHECK_MEMBERS([struct stat.st_rdev])
AC_TYPE_UINT64_T

# Checks for library functions.
AC_FUNC_ALLOCA
AC_FUNC_CHOWN
AC_FUNC_FORK
AC_FUNC_GETMNTENT
AC_FUNC_LSTAT dnl# also checks whether it "_FOLLOWS_SLASHED_SYMLINK"
AC_FUNC_MALLOC
AC_FUNC_MKTIME
AC_FUNC_MMAP
AC_FUNC_REALLOC
AC_CHECK_FUNCS([atexit bzero fdatasync ftruncate getcwd gethostname lchown \
                memmove memset mkdir munmap realpath rmdir select setlocale \
                socket strcasecmp strchr strcspn strdup strerror strtol \
                strtoull utime])dnl

if test "x${ac_cv_func_alarm}" = "x"; then
  test -z "${ac_cv_func_alarm}"
  AC_CHECK_FUNCS([alarm])
fi
if test "x${ac_cv_func_getmntent}" = "x"; then
  test -z "${ac_cv_func_getmntent}"
  AC_CHECK_FUNCS([getmntent])
fi
if test "x${ac_cv_func_getpagesize}" = "x"; then
  test -z "${ac_cv_func_getpagesize}"
  AC_CHECK_FUNCS([getpagesize])
fi

# Packages:
AC_PACKAGE_GLOBALS([xfsdump])
AC_PACKAGE_UTILITIES([xfsdump])
AC_MULTILIB([$enable_lib64])

AC_PACKAGE_NEED_UUID_H
AC_PACKAGE_NEED_UUIDCOMPARE

AC_PACKAGE_NEED_PTHREAD_H
AC_PACKAGE_NEED_PTHREADMUTEXINIT

AC_PACKAGE_NEED_NCURSES_H
AC_PACKAGE_WANT_WORKING_LIBNCURSES

AC_PACKAGE_NEED_XFS_XFS_H
AC_PACKAGE_NEED_XFS_HANDLE_H
AC_PACKAGE_NEED_OPEN_BY_FSHANDLE

AC_PACKAGE_NEED_ATTRIBUTES_H
AC_PACKAGE_NEED_ATTRIBUTES_MACROS
AC_PACKAGE_NEED_ATTRGET_LIBATTR

AC_MANUAL_FORMAT

# Output.
AC_CONFIG_FILES([include/builddefs])
AC_OUTPUT
