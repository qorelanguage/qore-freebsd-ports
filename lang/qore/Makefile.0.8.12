# $FreeBSD: head/lang/qore/Makefile 395028 2015-08-22 11:25:45Z bofh $

PORTNAME=       qore
PORTVERSION=    0.8.12
DISTNAME=       ${PORTNAME}-release-${PORTVERSION}
CATEGORIES=     lang
USE_GITHUB=     yes
GH_ACCOUNT=     qorelanguage
WRKSRC=         work/${GH_ACCOUNT}-${PORTNAME}-bc7adb8

MAINTAINER=     estrabd@gmail.com
COMMENT=        The Qore Programming Language

LICENSE=        MIT

LIB_DEPENDS=    libpcre.so:${PORTSDIR}/devel/pcre \
                libmpfr.so:${PORTSDIR}/math/mpfr
BUILD_DEPENDS=  ${LOCALBASE}/bin/flex:${PORTSDIR}/textproc/flex \
                ${LOCALBASE}/bin/bison:${PORTSDIR}/devel/bison

USES=           gmake iconv libtool:build pathfix
USE_OPENSSL=    yes
USE_LDCONFIG=   yes
GNU_CONFIGURE=  yes
# to add depedencies on required autotools; they are executed manually in the pre-configure target below
USE_AUTOTOOLS=  libtoolize:env aclocal:env autoconf:env autoheader:env automake:env

CONFIGURE_ENV=  LEX="${LOCALBASE}/bin/flex" PTHREAD_LIBS="-lpthread"
CONFIGURE_ARGS= --disable-debug --disable-static --with-doxygen=no
LDFLAGS+=       -L${LOCALBASE}/lib

PLIST_SUB=      PORTVERSION=${PORTVERSION}
INSTALL_TARGET= install-strip

.include <bsd.port.pre.mk>

.if ${ARCH} == "powerpc"
BROKEN=         Does not compile on powerpc
.endif

pre-configure:
	cd ${WRKSRC}; ./reconf.sh

post-configure:
	${REINPLACE_CMD} -e 's|; make|; $${MAKE}|g' ${WRKSRC}/Makefile.in

.include <bsd.port.post.mk>
