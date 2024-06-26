#
#
# Copyright (c) 2010 Apple Inc. All rights reserved.
#
# @APPLE_LICENSE_HEADER_START@
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
#
# 1.  Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
# 2.  Redistributions in binary form must reproduce the above copyright
#     notice, this list of conditions and the following disclaimer in the
#     documentation and/or other materials provided with the distribution.
# 3.  Neither the name of Apple Inc. ("Apple") nor the names of its
#     contributors may be used to endorse or promote products derived from
#     this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY APPLE AND ITS CONTRIBUTORS "AS IS" AND ANY
# EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
# WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL APPLE OR ITS CONTRIBUTORS BE LIABLE FOR ANY
# DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
# LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
# ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF
# THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
# Portions of this software have been released under the following terms:
#
# (c) Copyright 1989-1993 OPEN SOFTWARE FOUNDATION, INC.
# (c) Copyright 1989-1993 HEWLETT-PACKARD COMPANY
# (c) Copyright 1989-1993 DIGITAL EQUIPMENT CORPORATION
#
# To anyone who acknowledges that this file is provided "AS IS"
# without any express or implied warranty:
# permission to use, copy, modify, and distribute this file for any
# purpose is hereby granted without fee, provided that the above
# copyright notices and this notice appears in all source code copies,
# and that none of the names of Open Software Foundation, Inc., Hewlett-
# Packard Company or Digital Equipment Corporation be used
# in advertising or publicity pertaining to distribution of the software
# without specific, written prior permission.  Neither Open Software
# Foundation, Inc., Hewlett-Packard Company nor Digital
# Equipment Corporation makes any representations about the suitability
# of this software for any purpose.
#
# Copyright (c) 2007, Novell, Inc. All rights reserved.
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
#
# 1.  Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
# 2.  Redistributions in binary form must reproduce the above copyright
#     notice, this list of conditions and the following disclaimer in the
#     documentation and/or other materials provided with the distribution.
# 3.  Neither the name of Novell Inc. nor the names of its contributors
#     may be used to endorse or promote products derived from this
#     this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY
# EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
# WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR CONTRIBUTORS BE LIABLE FOR ANY
# DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
# LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
# ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF
# THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
# @APPLE_LICENSE_HEADER_END@
#
#

dnl Process this file with autoconf to produce a configure script.

AC_PREREQ([2.13])
AC_INIT([DCE RPC], [1.1.0.7])
AC_CONFIG_AUX_DIR([build])
AC_CONFIG_MACRO_DIR([m4])
AC_CANONICAL_TARGET

# reduce linux* to linux-gnu for target_os
# reduce hpux11.* to hpux11.11
# reduce freebsd 6.x/7.x/8.x to 6.0
case $target_os in
     linux*)   target_os="linux-gnu";;
     hpux11.*) target_os="hpux11.11";;
     darwin*) target_os="darwin";;
     solaris2.1*) target_os="solaris2.10";;
     freebsd6.*|freebsd7.*|freebsd8.*) target_os="freebsd6.0";;
esac

AC_SUBST(target_cpu)
AC_SUBST(target_os)

if test "x$SDKROOT" = "x" ; then
    SDKROOT=/
fi

AC_DEFINE_UNQUOTED([SDKROOT], ["$SDKROOT"], [Apple SDKROOT we are building against])
AC_SUBST(SDKROOT, $SDKROOT)

# Note, we use -Wno-portability to disable warnings about GNU make-specific rules.
AM_INIT_AUTOMAKE([1.11 -Wall -Wno-portability silent-rules foreign subdir-objects])
AM_MAINTAINER_MODE([enable])
AM_SILENT_RULES([yes])

AM_PROG_AR

LT_INIT([disable-static pic-only dlopen])

# AC_PREFIX_DEFAULT(/opt/dcerpc)
AC_PREFIX_DEFAULT(/usr/local)
AC_CONFIG_SRCDIR([uuid/uuid.c])
AC_CONFIG_HEADER([include/config.h])

AM_DISABLE_STATIC

dnl Checks for programs.
AC_PROG_CC
AC_PROG_CPP
AC_PROG_CXX
AC_PROG_AWK
AM_PROG_LIBTOOL
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_SED
AC_PATH_PROG(GENCAT, gencat, true)
AC_PATH_PROG(XCRUN, xcrun)
AC_SUBST(GENCAT)
AC_OBJEXT
AC_C_INLINE
XAC_C_ATTRIBUTE_UNUSED

AC_ARG_VAR([FLEX], [Flex lexer generator command])
AC_PATH_PROG([FLEX],[flex])
AX_PROG_FLEX_VERSION([2.5.35], [], AC_MSG_ERROR([Flex version 2.5.35 or later is required]))

# We need at Bison >= 2.4 for the %name-prefix directive.
AC_ARG_VAR([BISON], [Bison parser generator command])
AC_PATH_PROG([BISON], [bison])
AX_PROG_BISON_VERSION([2.4.0], [], AC_MSG_ERROR([Bison version 2.4 or later is required]))

AX_CFLAGS_GCC_OPTION(-fno-strict-aliasing)

AX_CFLAGS_GCC_OPTION(-Wall)
AX_CFLAGS_GCC_OPTION(-Wextra)
AX_CFLAGS_GCC_OPTION(-Wshorten-64-to-32)
AX_CFLAGS_GCC_OPTION(-Wmissing-format-attribute)
AX_CFLAGS_GCC_OPTION(-Wbad-function-cast)
AX_CFLAGS_GCC_OPTION(-Wstrict-prototypes)
AX_CFLAGS_GCC_OPTION(-Wpointer-arith)
AX_CFLAGS_GCC_OPTION(-Wcast-align)
AX_CFLAGS_GCC_OPTION(-Wwrite-strings)

# On Linux with autoconf 2.67, passing options with an embedded '=' gives
# autoconf a fit and causes it to put variable names like '31078as_VAR'
# into CFLAGS. Go figure -- jpeach
case $target_os in
     darwin*) AX_CFLAGS_GCC_OPTION(-Wformat=2) ;;
esac

# If we have a gcc that does stack protection, also enable
# string API function checking.
AX_CFLAGS_GCC_OPTION(-fstack-protector, [],
    [
	CFLAGS="$CFLAGS -fstack-protector";
	CPPFLAGS="$CPPFLAGS -D_FORTIFY_SOURCE=2";
    ])

# Specify desired UNIX interface
case "$target_os" in
     *darwin*)
		FEATURETEST_CFLAGS="-D_SOCKADDR_LEN"
		IDL_CFLAGS="$IDL_CFLAGS -D_SOCKADDR_LEN"

		# For Intel architectures, we need to be explicit
		# to make sure the compiler builds the sub architecture
		# we want on systems that support more than one.
		case $target_cpu in
		    i386) AX_CFLAGS_GCC_OPTION(-arch i386) ;;
		    x86_64) AX_CFLAGS_GCC_OPTION(-arch x86_64) ;;
		    ppc|powerpc) AX_CFLAGS_GCC_OPTION(-arch ppc) ;;
		    ppc64|powerpc64) AX_CFLAGS_GCC_OPTION(-arch ppc64) ;;
		esac

		# We need to use the generic arch headers so that we can
		# merge them during fat builds.
		target_cpu=generic
		;;
     *freebsd*)
		FEATURETEST_CFLAGS="-D_SOCKADDR_LEN"
		IDL_CFLAGS="$IDL_CFLAGS -D_SOCKADDR_LEN"
		;;
     *aix*)
                FEATURETEST_CFLAGS="-D_XOPEN_SOURCE=500 -D_ALL_SOURCE=1 -D_REENTRANT"
		IDL_CFLAGS="$IDL_CFLAGS -D_SOCKADDR_LEN"
		;;
     *) FEATURETEST_CFLAGS="-D_XOPEN_SOURCE=500 -D__EXTENSIONS__ -D_POSIX_PTHREAD_SEMANTICS -D_ALL_SOURCE=1 -D_REENTRANT" ;;
esac

AC_SUBST([FEATURETEST_CFLAGS])
AC_DEFINE([FEATURETEST_CFLAGS], [$FEATURETEST_CFLAGS], [Feature test flags])

CPPFLAGS="$CPPFLAGS $FEATURETEST_CFLAGS"

# Allow libtool-specific linker flags to be passed in
AC_SUBST(LTLDFLAGS)

dnl Checks for libraries.
AC_CHECK_LIB(socket,		socket,		 [LIB_socket="-lsocket" AC_SUBST(LIB_socket)],,)
AC_CHECK_LIB(nsl,		gethostbyname,	 [LIB_nsl="-lnsl"],,)
AC_CHECK_LIB(dl,		dlopen,		 [LIB_dl="-ldl" AC_SUBST(LIB_dl)],,)
AC_SUBST(LIB_nsl)

dnl Checks for header files.
AC_CHECK_HEADERS(features.h sys/cdefs.h dlfcn.h sys/time.h)
AC_CHECK_HEADERS(getopt.h sys/sockio.h sys/un.h nl_types.h)
AC_CHECK_HEADERS(net/if_dl.h execinfo.h sys/fd_set.h)

AC_CHECK_FUNCS(scandir getpeereid)

dnl Check for number of arguments to gethostbyname_r
saved_LIBS="$LIBS"
LIBS="$LIBS $LIB_nsl"
AC_CHECK_FUNCS(gethostbyname_r)
if test "$ac_cv_func_gethostbyname_r" = "yes"; then
AC_CACHE_CHECK(number of arcuments to gethostbyname_r, xad_cv_gethostbyname_r_args, [
xad_cv_gethostbyname_r_args=
   AC_TRY_COMPILE([
#include <netdb.h>], [gethostbyname_r(0, 0, 0, 0, 0, 0);], [xad_cv_gethostbyname_r_args=6], [
         AC_TRY_COMPILE([
		#include <netdb.h>],
		[gethostbyname_r(0, 0, 0, 0, 0);], [xad_cv_gethostbyname_r_args=5], [xad_cv_gethostbyname_r_args=3])]) ])
fi
AC_DEFINE_UNQUOTED(GETHOSTBYNAME_R_ARGS, $xad_cv_gethostbyname_r_args, Number of arguments to gethostbyname_r)
LIBS="$saved_LIBS"

dnl Checks for typedefs, structures, and compiler characteristics.

dnl Checks for library functions.

dnl _GNU_SOURCE pulls in the definition of _pthread_push_defer
AC_DEFINE(__EXTENSIONS__, 1, Ask for extension api)
AC_DEFINE(_REENTRANT, 1, Ask for re-entrant api)
AC_DEFINE(_GNU_SOURCE, 1, Ask for gnu extensions)
AC_DEFINE(_BSD, 1, Tell libc that we want BSD things)

RPC_ARG_DEFINE(debug, DEBUG, yes, [Compile with debugging support])
RPC_ARG_DEFINE(dcom, ENABLE_DCOM, no,[Enable experimental DCOM support])
AM_CONDITIONAL(ENABLE_DCOM, test x$rpc_arg_dcom = yes)
AM_CONDITIONAL(TARGET_OS_LINUX, test x$target_os = xlinux-gnu)
AM_CONDITIONAL(TARGET_OS_DARWIN, test x$target_os = xdarwin)

AC_CHECK_FUNCS(pthread_setugid_np)
AC_CHECK_HEADERS(sys/kauth.h sys/syscall.h)

AC_CHECK_FUNCS(strlcpy strlcat)

if test x"$localstatedir" = x"/var"; then
    rpccachedir="$localstatedir/lib/likewise"
else
    rpccachedir="$localstatedir"
fi
AS_AC_EXPAND(rpc_dir, ["$rpccachedir/rpc"])

AC_CACHE_CHECK([for named pipes directory],
	[rpcd_cv_rpc_c_np_dir],
	[rpcd_cv_rpc_c_np_dir="$rpc_dir"])

AC_CACHE_CHECK([for unix domain sockets directory],
	[rpcd_cv_rpc_c_uxd_dir],
	[rpcd_cv_rpc_c_uxd_dir="$rpc_dir"])

AC_DEFINE_UNQUOTED([RPC_C_NP_DIR], ["$rpcd_cv_rpc_c_np_dir"], [named pipes directory])
AC_DEFINE_UNQUOTED([RPC_C_UXD_DIR], ["$rpcd_cv_rpc_c_uxd_dir"], [unix domain sockets directory])

#####################################################################
## COMPONENT: threads

AC_MSG_CHECKING(pthread library and requirements)
AC_MSG_RESULT()

AC_ARG_WITH(pthread-ext-dir,
	AC_HELP_STRING([--with-pthread-ext-dir=DIR],
		       [base directory of pthread extension library]))

AC_ARG_WITH(pthread-ext-libdir,
	AC_HELP_STRING([--with-pthread-ext-libdir=DIR],
		       [directory of pthread extension library (defaults to --with-pthread-ext-dir/lib)]))

if test -n "$with_pthread_ext_dir"; then
  CPPFLAGS="$CPPFLAGS -I$with_pthread_ext_dir/include"
  LDFLAGS="$LDFLAGS -L$with_pthread_ext_dir/lib"
  if test -z "$with_pthread_ext_libdir"; then
    with_pthread_ext_libdir="$with_pthread_ext_dir/lib"
  fi
fi

if test -n "$with_pthread_ext_libdir"; then
  LDFLAGS="$LDFLAGS -L$with_pthread_ext_libdir"
fi

AC_ARG_WITH(pthread-ext-rpath,
	AC_HELP_STRING([--with-pthread-ext-rpath=DIR],
		[directory where the pthread extension will be installed at runtime (defaults to --with-pthread-ext-libdir value)]),
    [pthread_ext_rpath="$withval"],
    [pthread_ext_rpath="$with_pthread_ext_libdir"])

if test -n "$pthread_ext_rpath"; then
  LIBTOOLFLAGS="$LIBTOOLFLAGS -rpath $pthread_ext_rpath"
fi

AC_CHECK_HEADERS(pthread.h)

if test -n "$with_pthread_ext_dir"; then
   AC_CHECK_HEADERS(pthread_ext.h)
fi

AC_CHECK_LIB(pthread,		pthread_create,		[LIB_pthread="-lpthread" AC_SUBST(LIB_pthread)],,)

PTHREAD_MODE="none"

AC_CHECK_LIB(rt, sched_yield, [LIB_rt="-lrt" AC_SUBST(LIB_rt)],,)

dcethreads_save_LIBS="$LIBS"
LIBS="$LIBS $LIB_pthread $LIB_rt"

AC_CHECK_FUNCS(pthread_atfork)
AC_CHECK_FUNCS(pthread_get_expiration_np)
AC_CHECK_FUNCS(pthread_delay_np)
AC_CHECK_FUNCS(pthread_lock_global_np)
AC_CHECK_FUNCS(pthread_unlock_global_np)
AC_CHECK_FUNCS(pthread_getunique_np)
AC_CHECK_FUNCS(pthread_ismultithreaded_np)
AC_CHECK_FUNCS(pthread_kill_other_threads_np)
AC_CHECK_FUNCS(pthread_mutexattr_getkind_np)
AC_CHECK_FUNCS(pthread_mutexattr_setkind_np)
AC_CHECK_FUNCS(pthread_yield)
AC_CHECK_FUNCS(sched_yield)
AC_CHECK_FUNCS(vasprintf)

AC_SUBST(DCETHREADINCLUDES)

LIBS="$dcepthreads_save_LIBS"

AC_CHECK_FUNCS(backtrace backtrace_symbols backtrace_symbols_fd)

#####################################################################
## COMPONENT: uuid

AC_MSG_CHECKING(UUID library and tool requirements)
AC_MSG_RESULT()

AC_CHECK_HEADERS(sys/sysctl.h)
AC_CHECK_HEADERS(net/if_arp.h)
AC_CHECK_FUNCS(gettimeofday socket)

#####################################################################
## COMPONENT: include

if test "x$ENABLE_DCOM" = "xyes" ; then
	include_dcom_idl="objex.idl obase.idl remact.idl wtypes.idl"
else
	include_dcom_idl=""
fi
AC_SUBST(include_dcom_idl)

#####################################################################
## COMPONENT: idl/idl_compiler

RPC_ARG_DEFINE(idldumpers, DUMPERS, no, [Enable DUMPERS for debugging dceidl])
AC_CHECK_FUNCS(catopen)

dnl IDL needs to set these flags when it compiles stuff
IDL_CFLAGS="$IDL_CFLAGS -D_GNU_SOURCE -D_REENTRANT -D_POSIX_C_SOURCE=3"
AC_SUBST(IDL_CFLAGS)

dnl For DCOM, default to C++ compiler for now
if test "x$ENABLE_DCOM" = "xyes" ; then
	IDL_CC=" $CXX"
else
	IDL_CC=" $CC"
fi

dnl If using GCC, we need to add -x c-header to force it to treat idl files
dnl as C headers; otherwise it tries to do something wierd...
if test "x${ac_cv_prog_gcc}" = "xyes" ; then
	IDL_CPP="$CPP -x c-header"
else
	IDL_CPP="$CPP"
fi

# On Darwin, we default the IDL compiler to the default toolchain so that you
# can do "configure CC=~/bin/cc" and still use xcrun for building the IDL.
case $target_os in
    darwin*)
	IDL_CPP="${XCRUN} cc -E -x c-header"
	if test "x$ENABLE_DCOM" = "xyes" ; then
	    IDL_CC="${XCRUN} c++"
	else
	    IDL_CC="${XCRUN} cc"
	fi
	;;
esac

AC_SUBST(IDL_CPP)
AC_SUBST(IDL_CC)

#####################################################################
## COMPONENT: AUTH PLUGINS

##
## gss_negotiate

AC_ARG_WITH(
	gssapi-dir,
	AC_HELP_STRING([--with-gssapi-dir=DIR], [look for gssapi libraries in DIR]),
	[
	    GSSAPI_INCLUDES="-I$withval/include"
	    GSSAPI_LDFLAGS="-L$withval/`basename $libdir`"
	],
)

AC_ARG_WITH(
	gssapi-libdir,
	AC_HELP_STRING([--with-gssapi-libdir=DIR], [look for gssapi libraries in DIR]),
	[
	    GSSAPI_LDFLAGS="-L$withval"
	],
)

AX_CHECK_FRAMEWORK(GSS, [rpc_have_gss_framework=yes], [])
AX_CHECK_FRAMEWORK(Kerberos, [rpc_have_kerberos_framework=yes], [])

AC_SUBST(GSSAPI_INCLUDES)
AC_SUBST(GSSAPI_LDFLAGS)
AC_SUBST(GSSAPI_LIBS)

AC_CHECK_HEADERS(krb5.h gssapi/gssapi.h gssapi/gssapi_krb5.h gssapi/gssapi_ext.h)

tmp_LDFLAGS="$LDFLAGS"
LDFLAGS="$GSSAPI_LDFLAGS $LDFLAGS"
AC_CHECK_LIB(gssapi_krb5, gss_wrap, [GSSAPI_LIBS="-lgssapi_krb5"], [])
LDFLAGS="$tmp_LDFLAGS"

##
## schannel

AC_ARG_WITH(
	schannel-dir,
	AC_HELP_STRING([--with-schannel-dir=DIR], [look for libschannel in DIR]),
	[
	    SCHANNEL_INCLUDES="-I$withval/include"
	    SCHANNEL_LDFLAGS="-L$withval/`basename $libdir`"
	],
)

AC_ARG_WITH(
	schannel-libdir,
	AC_HELP_STRING([--with-schannel-libdir=DIR], [look for libschannel libraries in DIR]),
	[
	    SCHANNEL_LDFLAGS="-L$withval"
	],
)

AC_SUBST(SCHANNEL_INCLUDES)
AC_SUBST(SCHANNEL_LDFLAGS)
AC_SUBST(SCHANNEL_LIBS)

tmp_LDFLAGS="$LDFLAGS"
LDFLAGS="$SCHANNEL_LDFLAGS $LDFLAGS"
AC_CHECK_LIB(schannel, schn_wrap, [SCHANNEL_LIBS="-lschannel"])
LDFLAGS="$tmp_LDFLAGS"

#####################################################################
## COMPONENT: ncklib

# Keep track of whether we have a library that will provide a ncacn_np
# transport.
rpc_have_np_transport=no

#
# Check to see whether SMBClient framework is available or not
#
rpc_have_smbclient_framework=yes
RPC_SMBCLIENT_FRAMEWORK(NAF_NP_CPPFLAGS, NAF_NP_LDFLAGS, NAF_NP_LIBS,
	rpc_have_smbclient_framework=no)

AM_CONDITIONAL(HAVE_SMBCLIENT_FRAMEWORK,
	test x${rpc_have_smbclient_framework} = xyes)
if test x${rpc_have_smbclient_framework} = xyes ; then
    rpc_have_np_transport=yes
    AC_DEFINE(HAVE_SMBCLIENT_FRAMEWORK, 1,
	    [whether the SMBClient.framework API is available])
fi

# Check whether the Likewise SMB named pipe client library is available. If so,
# we need to link it for named pipe support.
AC_CHECK_HEADERS([lwio/lwio.h])
AC_CHECK_LIB(lwioclient, LwNtCtxCreateNamedPipeFile,
	[
	    NAF_NP_LIBS="-llwioclient"
	    rpc_have_likewise_lwio=yes
	    rpc_have_np_transport=yes
	    AC_DEFINE(HAVE_LIKEWISE_LWIO, 1,
		    [whether the Likewise lwioclient API is available])
	],
	[
	    rpc_have_likewise_lwio=no
	])

AM_CONDITIONAL(HAVE_LIKEWISE_LWIO, test x${rpc_have_likewise_lwio} = xyes)

AC_SUBST(NAF_NP_CPPFLAGS)
AC_SUBST(NAF_NP_LDFLAGS)
AC_SUBST(NAF_NP_LIBS)

RPC_ARG_DEFINE(ncacn, PROT_NCACN, yes,Support connection based transports)
if test x"$rpc_arg_ncacn" = xyes
then
	AC_DEFINE([ENABLE_PROT_NCACN], [], [Enable NCACN protocol sequence])
fi
AM_CONDITIONAL(PROT_NCACN, test x${rpc_arg_ncacn} = xyes)

RPC_ARG_DEFINE(ncadg, PROT_NCADG, yes,Support connectionless transports)
if test x"$rpc_arg_ncadg" = xyes
then
	AC_DEFINE([ENABLE_PROT_NCADG], [], [Enable NCADG protocol sequence])
fi
AM_CONDITIONAL(PROT_NCADG, test x${rpc_arg_ncadg} = xyes)

RPC_ARG_DEFINE(dummyauth, AUTH_DUMMY, no,Include the DCE dummy auth service)
AM_CONDITIONAL(AUTH_DUMMY, test x${rpc_arg_dummyauth} = xyes)

if test "x${rpc_arg_dummyauth}" = "xyes" ; then
	AUTH_DUMMY_EXTRAS=""
	test "x${rpc_arg_ncacn}" = "xyes" && AUTH_DUMMY_EXTRAS="$AUTH_DUMMY_EXTRAS noauthcn.c"
	test "x${rpc_arg_ncadg}" = "xyes" && AUTH_DUMMY_EXTRAS="$AUTH_DUMMY_EXTRAS noauthdg.c"
	AC_SUBST(AUTH_DUMMY_EXTRAS)
fi

# If we have anything that looks like GSSAPI libraries, default the
# gss_negotiate auth module to yes. Otherwise, default it to no and
# let the user override the default.

if test "x${rpc_have_gss_framework}" = "xyes" -o \
	"x${ac_cv_lib_gssapi_krb5_gss_wrap}" = "xyes" ; then
    rpc_default_gss_negotiate=yes
else
    rpc_default_gss_negotiate=no
fi

RPC_ARG_DEFINE(gss_negotiate, AUTH_GSS_NEGOTIATE, auto, Include the DCE gss_negotiate auth service)
if test x"$rpc_arg_gss_negotiate" = xyes
then
	AC_DEFINE([ENABLE_AUTH_GSS_NEGOTIATE], [], [Enable GSS negotiate auth mechanism])
fi
AM_CONDITIONAL(AUTH_GSS_NEGOTIATE, test x${rpc_arg_gss_negotiate} = xyes)

# If we found libschannel, build it by default, otherwise disable it by
# default.
RPC_ARG_DEFINE(schannel, AUTH_SCHANNEL, auto, Include the schannel auth service)
if test x"$rpc_arg_schannel" = xyes
then
	AC_DEFINE([ENABLE_AUTH_SCHANNEL], [], [Enable schannel auth mechanism])
fi
AM_CONDITIONAL(AUTH_SCHANNEL, test x${rpc_arg_schannel} = xyes)

# Make sure that we actually have libschannel if it was force-enabled.
if test "x${rpc_arg_schannel}" = "xyes" -a \
       "x${ac_cv_lib_schannel_schn_wrap}" != "xyes" ; then
    AC_MSG_ERROR([Could not find libschannel])
fi

RPC_ARG_DEFINE(codeset, BUILD_CODESET, no,Support for the codeset registry (untested))
AM_CONDITIONAL(BUILD_CODESET, test x${rpc_arg_codeset} = xyes)

RPC_ARG_DEFINE(rpc-ns-ldap, BUILD_RPC_NS_LDAP, no,Support for the LDAP nameservice (untested))
AM_CONDITIONAL(BUILD_RPC_NS_LDAP, test x${rpc_arg_rpc_ns_ldap} = xyes)
AC_CHECK_FUNCS(scandir)

RPC_ARG_DEFINE(afip, NAF_IP, yes,IP network address family support)
if test x"$rpc_arg_afip" = xyes
then
	AC_DEFINE([ENABLE_NAF_IP], [], [Enable IP address family support])
fi
AM_CONDITIONAL(NAF_IP, test x${rpc_arg_afip} = xyes)

RPC_ARG_DEFINE(afnp, NAF_NP,yes,Named Pipes network address family support)
if test x"$rpc_arg_afnp" = xyes
then
	AC_DEFINE([ENABLE_NAF_NP], [], [Enable named pipe address family support])
fi

AM_CONDITIONAL(NAF_NP, test x${rpc_arg_afnp} = xyes)

if test "x${rpc_arg_afnp}" = "xyes" -a \
	"x${rpc_have_np_transport}" != "xyes" ; then
    AC_MSG_WARN(Enabling the named pipe transport without SMB pipe support)
fi

RPC_ARG_DEFINE(afuxd, NAF_UXD,no,AF_LOCAL network address family support (untested))
AM_CONDITIONAL(NAF_UXD, test x${rpc_arg_afuxd} = xyes)

RPC_ARG_DEFINE(ifloopback, USE_LOOPBACK, yes,Include loopback interface support)

# Check whether the Likewise lwmapsecurity library is available for
# access token support
AC_CHECK_HEADERS([lw/base.h, lwmapsecurity/lwmapsecurity.h])
AC_CHECK_LIB(lwmapsecurity, LwMapSecurityInitialize,
	[
	    rpc_have_likewise_lwmapsecurity=yes
	    AC_DEFINE(HAVE_LIKEWISE_LWMAPSECURITY, 1,
		    [whether the Likewise lwmapsecurity API is available])
	],
	[
	    rpc_have_likewise_lwmapsecurity=no
	])

AM_CONDITIONAL(HAVE_LIKEWISE_LWMAPSECURITY,
	test x${rpc_have_likewise_lwmapsecurity} = xyes)

#####################################################################
## COMPONENT: dcelib

RPC_LIBUNISTR(CPPFLAGS_unistr, LDFLAGS_unistr, LIB_unistr,
       AC_MSG_WARN([cannot find a UNICODE converter]))

dnl XXX Add Linux unicode support using GNU libunistring?

AC_SUBST(CPPFLAGS_unistr)
AC_SUBST(LDFLAGS_unistr)
AC_SUBST(LIB_unistr)

#####################################################################
## COMPONENT: rpcd

AS_AC_EXPAND(SBINDIR, ["${sbindir}"])

AC_CHECK_FUNCS(setpgrp)
if test "$ac_cv_func_setpgrp" = "yes"; then
	AC_CACHE_CHECK(whether setpgrp() takes 2 arguments, rpcd_cv_setpgrp_args, [
		AC_TRY_COMPILE([#include <unistd.h>], [setpgrp(0, 0);], [rpcd_cv_setpgrp_args=2], [rpcd_cv_setpgrp_args=0])])
	AC_DEFINE_UNQUOTED(SETPGRP_ARGS, $rpcd_cv_setpgrp_args, Number of arguments to setgrp())
fi

#####################################################################
## COMPONENT: demos

RPC_ARG_DEFINE(demoprogs, DEMO_PROGS, yes,Build demo programs)

#####################################################################

#####
## Unit tests
#####

# Check for moonunit bits
AC_CHECK_HEADERS([moonunit/moonunit.h], [HAVE_MOONUNIT_H=true], [HAVE_MOONUNIT_H=false])
AC_CHECK_LIB(moonunit, Mu_Interface_Result, [HAVE_MOONUNIT_LIB=true], [HAVE_MOONUNIT_LIB=false])
AC_CHECK_PROG(MOONUNIT_STUB, moonunit-stub, moonunit-stub, false)

if test "${MOONUNIT_STUB}" = "moonunit-stub" && $HAVE_MOONUNIT_H && $HAVE_MOONUNIT_LIB
then
	HAVE_MOONUNIT="true"
	LIB_moonunit="-lmoonunit"
	AC_DEFINE([HAVE_MOONUNIT], [], [Have MoonUnit])
else
	HAVE_MOONUNIT="false"
fi

AC_SUBST(LIB_moonunit)
AM_CONDITIONAL(HAVE_MOONUNIT, $HAVE_MOONUNIT)

AC_OUTPUT(
Makefile
dnl freedce.spec
compat/Makefile
libdcethread/Makefile
uuid/Makefile
include/Makefile
include/compat/Makefile
include/dce/Makefile
include/dce/dce.h
include/dce/dce_error.h
include/dce/dce_utils.h
include/dce/marshall.h
include/dce/ndr_rep.h
include/dce/ndrtypes.h
include/dce/sec_authn.h
include/dce/aarch64/Makefile
include/dce/aix5.2.0.0/Makefile
include/dce/armv7l/Makefile
include/dce/darwin/Makefile
include/dce/linux-gnu/Makefile
include/dce/freebsd6.0/Makefile
include/dce/solaris2.8/Makefile
include/dce/solaris2.9/Makefile
include/dce/solaris2.10/Makefile
include/dce/hpux11.11/Makefile
include/dce/generic/Makefile
include/dce/i386/Makefile
include/dce/hppa2.0/Makefile
include/dce/powerpc/Makefile
include/dce/powerpc64/Makefile
include/dce/s390/Makefile
include/dce/s390x/Makefile
include/dce/sparc/Makefile
include/dce/x86_64/Makefile
include/dce/ia64/Makefile
idl_compiler/Makefile
idl_compiler/sysdep.h
idl_lib/Makefile
ncklib/Makefile
dcelib/Makefile
ncklib/include/aix5.2.0.0/Makefile
ncklib/include/linux-gnu/Makefile
ncklib/include/freebsd6.0/Makefile
ncklib/include/solaris2.8/Makefile
ncklib/include/solaris2.9/Makefile
ncklib/include/solaris2.10/Makefile
ncklib/include/darwin/Makefile
ncklib/include/hpux11.11/Makefile
ncklib/include/Makefile
rpcd/Makefile
rpcd/dcerpcd.reg
demos/Makefile
demos/echo_server/Makefile
demos/echo_number/Makefile
demos/echo_union/Makefile
demos/samr_test/Makefile
demos/access/Makefile
perf/Makefile
tools/Makefile
)
