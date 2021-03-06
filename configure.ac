m4_define([farmhash_major], [1])
m4_define([farmhash_minor], [1])
m4_define([farmhash_patchlevel], [0])

# Libtool shared library interface versions (current:revision:age)
# Update this value for every release!  (A:B:C will map to foo.so.(A-C).C.B)
# http://www.gnu.org/software/libtool/manual/html_node/Updating-version-info.html
m4_define([farmhash_ltversion], [2:0:0])

AC_PREREQ([2.65])
AC_INIT([FarmHash], [farmhash_major.farmhash_minor.farmhash_patchlevel], [farmhash-discuss@googlegroups.com])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([1.10 no-define foreign])
LT_PREREQ([2.2])
LT_INIT

AC_CONFIG_FILES([Makefile
                 src/Makefile])
AC_CONFIG_SRCDIR([src/farmhash.h])
AC_CONFIG_MACRO_DIR([m4])

AC_ARG_ENABLE([optional-builtin-expect],
              AS_HELP_STRING("Assume __builtin_expect() may or may not be available.  The default is to assume it is available."),
	      [ farmhash_optional_builtin_expect=true ],
	      [])
AM_CONDITIONAL([OPTIONAL_BUILTIN_EXPECT], [test x$farmhash_optional_builtin_expect = xtrue ])

AC_ARG_ENABLE([optional-builtin-bswap],
              AS_HELP_STRING("Assume __builtin_bswap32() and similar may or may not be available.  The default is to assume they are available."),
	      [ farmhash_optional_builtin_bswap=true ],
	      [])
AM_CONDITIONAL([OPTIONAL_BUILTIN_BSWAP], [test x$farmhash_optional_builtin_bswap = xtrue ])

# Checks for programs.
AC_PROG_CXX
AC_LANG([C++])
AC_C_BIGENDIAN

# Checks for libraries.

# Checks for header files.
AC_CHECK_HEADERS([stdint.h stdlib.h])

# Checks for typedefs, structures, and compiler characteristics.
#AC_C_INLINE
#AC_TYPE_SIZE_T
#AC_TYPE_SSIZE_T
#AC_TYPE_UINT32_T
#AC_TYPE_UINT64_T
#AC_TYPE_UINT8_T

# Check for __builtin_expect
AC_MSG_CHECKING([if the compiler supports __builtin_expect])
AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM(, [[return __builtin_expect(1, 1) ? 1 : 0;]])],
  [
    farmhash_have_builtin_expect=yes
    AC_MSG_RESULT([yes])
], [
    farmhash_have_builtin_expect=no
    AC_MSG_RESULT([no])
])
if test x$farmhash_have_builtin_expect = xyes ; then
    AC_DEFINE([HAVE_BUILTIN_EXPECT], [1], [Define to 1 if the compiler supports __builtin_expect.])
fi

# Check for __builtin_bswap32
AC_MSG_CHECKING([if the compiler supports __builtin_bswap32])
AC_COMPILE_IFELSE(
  [AC_LANG_PROGRAM(, [[return __builtin_bswap32(0xabcd1234) == 0x3412cdab ? 0 : 1;]])],
  [
    farmhash_have_builtin_bswap=yes
    AC_MSG_RESULT([yes])
], [
    farmhash_have_builtin_bswap=no
    AC_MSG_RESULT([no])
])
if test x$farmhash_have_builtin_bswap = xyes ; then
    AC_DEFINE([HAVE_BUILTIN_BSWAP], [1], [Define to 1 if the compiler supports __builtin_bswap32.])
fi

AC_OUTPUT

echo \
"-------------------------------------------------

${PACKAGE_NAME} Version ${PACKAGE_VERSION}

Prefix: '${prefix}'.
Compiler: '${CXX} ${CXXFLAGS}'

Now type 'make @<:@<target>@:>@'
  where the optional <target> is:
    all                - build everything
    check              - build and run tests
    install            - install everything

--------------------------------------------------"
