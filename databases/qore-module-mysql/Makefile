# $FreeBSD: head/lang/qore/Makefile 382211 2015-03-25 12:58:33Z marino $

#http://downloads.sourceforge.net/project/qore/module-mysql/2.0.1/qore-mysql-module-2.0.1.tar.bz2

PORTNAME=	qore-mysql-module
PORTVERSION=	2.0.1	
CATEGORIES=	lang
MASTER_SITES=	SF/qore/module-mysql/${PORTVERSION}/

MAINTAINER=	estrabd@gmail.com
COMMENT=	The Mysql client module for the Qore Programming Language

LICENSE=	GPLv2

LIB_DEPENDS=    libqore.so:${PORTSDIR}/lang/qore
                libmysqlclient.so:${PORTSDIR}/databases/mariadb-client

USES=		gmake libtool pathfix tar:bzip2
USE_LDCONFIG=	yes
GNU_CONFIGURE=	yes

CONFIGURE_ENV=	LEX="${LOCALBASE}/bin/flex" PTHREAD_LIBS="-lpthread"
CONFIGURE_ARGS=	--disable-debug --disable-static --with-doxygen=no
LDFLAGS+=	-L${LOCALBASE}/lib

PLIST_SUB=	PORTVERSION=${PORTVERSION}

.include <bsd.port.pre.mk>

.if ${ARCH} == "powerpc"
BROKEN=		Does not compile on powerpc
.endif

post-patch:
	${REINPLACE_CMD} -e 's|; make|; $${MAKE}|g' ${WRKSRC}/Makefile.in

.include <bsd.port.post.mk>
