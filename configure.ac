#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT(check_oracle_health,3.3.0.3-lm)
AM_INIT_AUTOMAKE([1.9 tar-pax])
AM_MAINTAINER_MODE([disable])
AC_CANONICAL_HOST
RELEASE=1
AC_SUBST(RELEASE)

AC_PREFIX_DEFAULT(/usr/local/nagios)

WARRANTY="This plugin comes with ABSOLUTELY NO WARRANTY. You may redistribute\ncopies of the plugin under the terms of the GNU General Public License.\nFor more information about these matters, see the file named COPYING.\n"
AC_SUBST(WARRANTY)

SUPPORT="Send email to gerhard.lausser@consol.de if you have questions\nregarding use of this software.\nPlease include version information with all correspondence (when possible,\nuse output from the --version option of the plugin itself).\n"
AC_SUBST(SUPPORT)

AC_ARG_WITH(nagios_user,
  ACX_HELP_STRING([--with-nagios-user=USER],
    [set user name to run nagios]),
  with_nagios_user=$withval,
  with_nagios_user=nagios)
AC_ARG_WITH(nagios_group,
  ACX_HELP_STRING([--with-nagios-group=GROUP],
    [set group name to run nagios]),
  with_nagios_group=$withval,
  with_nagios_group=nagios)
AC_SUBST(with_nagios_user)
AC_SUBST(with_nagios_group)
INSTALL_OPTS="-o $with_nagios_user -g $with_nagios_group"
AC_SUBST(INSTALL_OPTS)

AC_ARG_WITH(statefiles_dir,
  ACX_HELP_STRING([--with-statefiles-dir=PATH],
    [sets directory for the state files (default=/var/tmp/check_oracle_health)]),
  with_statefiles_dir=$withval,
  with_statefiles_dir=/var/tmp/check_oracle_health)
AC_SUBST(STATEFILES_DIR, $with_statefiles_dir)
echo variable with_statefiles_dir is $with_statefiles_dir

AC_ARG_WITH(mymodules_dir,
  ACX_HELP_STRING([--with-mymodules-dir=PATH],
    [sets directory for own extensions which will be included during the build process (default=/usr/local/nagios/libexec)]),
  with_mymodules_dir=$withval,
  with_mymodules_dir=/usr/local/nagios/libexec)
AC_SUBST(MYMODULES_DIR, $with_mymodules_dir)
echo variable with_mymodules_dir is $with_mymodules_dir

AC_ARG_WITH(mymodules_dyn_dir,
  ACX_HELP_STRING([--with-mymodules-dyn-dir=PATH],
    [sets directory for own extensions which will be included at runtime (default=/usr/local/nagios/libexec)]),
  with_mymodules_dyn_dir=$withval,
  with_mymodules_dyn_dir=/usr/local/nagios/libexec)
AC_SUBST(MYMODULES_DYN_DIR, $with_mymodules_dyn_dir)
echo variable with_mymodules_dyn_dir is $with_mymodules_dyn_dir


EXTRAS=
# PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/etc:/usr/local/bin:/usr/local/sbin:$PATH


# Checks for programs.
AC_PROG_MAKE_SET
# Figure out how to invoke "install" and what install options to use.
AC_PROG_INSTALL
AC_SUBST(INSTALL)
AC_PATH_PROG(ECHO,echo)
AC_PATH_PROG(SED,sed)
AC_PATH_PROG(GREP,grep)
AC_PATH_PROG(CAT,cat)
AC_PATH_PROG(SH,sh)
AC_PATH_PROG(PERL,perl)
AC_PATH_PROG(GZIP,gzip)
AC_PATH_PROGS(AWK,gawk nawk /usr/xpg4/bin/awk awk)
# allow them to override the path of perl
AC_ARG_WITH(perl,
  ACX_HELP_STRING([--with-perl=PATH],
    [sets path to perl executable]),
  with_perl=$withval,with_perl=$PERL)
AC_SUBST(PERL, $with_perl)

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_CONFIG_FILES([Makefile plugins-scripts/Makefile plugins-scripts/subst t/Makefile])
AC_OUTPUT
ACX_FEATURE([with],[perl])
ACX_FEATURE([with],[statefiles-dir])
ACX_FEATURE([with],[nagios-user])
ACX_FEATURE([with],[nagios-group])
ACX_FEATURE([with],[mymodules-dir])
ACX_FEATURE([with],[mymodules-dyn-dir])

