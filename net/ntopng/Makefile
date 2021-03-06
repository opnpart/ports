# Created by: Muhammad Moinur Rahman <5u623l20@gmail.com>
# $FreeBSD$

PORTNAME=	ntopng
PORTVERSION=	3.6.d201800910
PORTEPOCH=	1
CATEGORIES=	net

MAINTAINER=	madpilot@FreeBSD.org
COMMENT=	Network monitoring tool with command line and web interfaces

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

LIB_DEPENDS=	librrd.so:databases/rrdtool \
		libzmq.so:net/libzmq4 \
		libcurl.so:ftp/curl \
		libndpi.so:net/ndpi \
		libjson-c.so:devel/json-c \
		libsodium.so:security/libsodium \
		libmaxminddb.so:net/libmaxminddb
BUILD_DEPENDS=  bash:shells/bash

USE_HARDENING=	pie:off relro:off

USES=		autoreconf cpe gmake libtool localbase mysql pathfix pkgconfig \
		shebangfix sqlite ssl
SUB_FILES=	ntopng-geoipupdate.sh pkg-deinstall
SHEBANG_FILES=	httpdocs/misc/ntopng-add-user.sh \
		httpdocs/misc/ntopng-utils-manage-config.in
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-ndpi-includes=${LOCALBASE}/include/ndpi

USERS=		ntopng
GROUPS=		ntopng

USE_GITHUB=	yes
GH_ACCOUNT=	ntop
GH_TAGNAME=	96a403a

CPE_VENDOR=	ntop

OPTIONS_DEFINE=		GEOIP NLS
OPTIONS_DEFAULT=	GEOIP

OPTIONS_SUB=	yes

GEOIP_LIB_DEPENDS=	libGeoIP.so:net/GeoIP

NLS_USES=	gettext

USE_RC_SUBR=	ntopng

post-patch:
	@${REINPLACE_CMD} -e 's|%%LOCALBASE%%|${LOCALBASE}|' \
		${WRKSRC}/configure.seed
	@${REINPLACE_CMD} -e 's|^\(export PREFIX=\).*|\1 ${PREFIX}|' \
		${WRKSRC}/third-party/LuaJIT-2.1.0-git/Makefile
	cd ${WRKSRC} && ${SH} autogen.sh

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/ntopng

post-install-GEOIP-on:
	${INSTALL_SCRIPT} ${WRKDIR}/ntopng-geoipupdate.sh ${STAGEDIR}${PREFIX}/bin

.include <bsd.port.mk>
