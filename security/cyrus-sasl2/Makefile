# $FreeBSD$

PORTREVISION=	14

COMMENT=	RFC 2222 SASL (Simple Authentication and Security Layer)

USES=		cpe libtool:keepla pathfix perl5
USE_PERL5=	patch

CYRUS_CONFIGURE_ARGS=	--with-saslauthd=${SASLAUTHD_RUNPATH}

NO_OPTIONS_SORT=	yes
OPTIONS_DEFINE=		ALWAYSTRUE AUTHDAEMOND DOCS KEEP_DB_OPEN \
			OBSOLETE_CRAM_ATTR
OPTIONS_RADIO=		SASLDB
OPTIONS_RADIO_SASLDB=	BDB1 BDB GDBM
OPTIONS_GROUP=		PLUGIN
OPTIONS_GROUP_PLUGIN=	ANONYMOUS CRAM DIGEST LOGIN NTLM OTP PLAIN SCRAM
OPTIONS_DEFAULT=	ANONYMOUS AUTHDAEMOND BDB1 OBSOLETE_CRAM_ATTR CRAM \
			DIGEST LOGIN NTLM OTP PLAIN SCRAM
OPTIONS_SUB=		yes
ALWAYSTRUE_DESC=	Alwaystrue password verifier (discouraged)
ALWAYSTRUE_CONFIGURE_ENABLE=alwaystrue
AUTHDAEMOND_DESC=	Use of authdaemon
AUTHDAEMOND_CONFIGURE_ON=--with-authdaemond=/var/run/authdaemond/socket
AUTHDAEMOND_CONFIGURE_OFF=--with-authdaemond=no
KEEP_DB_OPEN_DESC=	Keep handle to Berkeley DB open
KEEP_DB_OPEN_CONFIGURE_ENABLE=keep-db-open
OBSOLETE_CRAM_ATTR_DESC=cmusaslsecretCRAM-MD5 auxprop property
OBSOLETE_CRAM_ATTR_CONFIGURE_OFF=--enable-obsolete_cram_attr=no
SASLDB_DESC=		SASLdb auxprop plugin
BDB_USES=		bdb
BDB_CONFIGURE_ON=	--with-dblib=berkeley \
			--with-bdb-libdir=${BDB_LIB_DIR} \
			--with-bdb-incdir=${BDB_INCLUDE_DIR} \
			--with-bdb=${BDB_LIB_NAME}
BDB1_CONFIGURE_ON=	--with-dblib=ndbm
GDBM_LIB_DEPENDS=	libgdbm.so:databases/gdbm
GDBM_CONFIGURE_ON=	--with-dblib=gdbm \
			--with-gdbm=${LOCALBASE}
ANONYMOUS_DESC=			ANONYMOUS authentication
ANONYMOUS_CONFIGURE_ENABLE=	anon
CRAM_DESC=		CRAM-MD5 authentication
CRAM_CONFIGURE_ENABLE=	cram
DIGEST_DESC=		DIGEST-MD5 authentication
DIGEST_CONFIGURE_ENABLE=digest
LOGIN_DESC=		LOGIN authentication
LOGIN_CONFIGURE_ENABLE=	login
NTLM_DESC=		NTLM authentication
NTLM_CONFIGURE_ENABLE=	ntlm
OTP_DESC=		OTP authentication
OTP_CONFIGURE_ENABLE=	otp
PLAIN_DESC=		PLAIN authentication
PLAIN_CONFIGURE_ENABLE=	plain
SCRAM_DESC=		SCRAM authentication
SCRAM_CONFIGURE_ENABLE=	scram

DOCS=	AUTHORS COPYING ChangeLog INSTALL INSTALL.TXT NEWS README

DOC2=	ONEWS TODO draft-burdis-cat-srp-sasl-xx.txt \
	draft-ietf-sasl-anon-xx.txt draft-ietf-sasl-crammd5-xx.txt \
	draft-ietf-sasl-gssapi-xx.txt draft-ietf-sasl-plain-xx.txt \
	draft-ietf-sasl-rfc2222bis-xx.txt draft-ietf-sasl-rfc2831bis-xx.txt \
	draft-ietf-sasl-saslprep-xx.txt draft-murchison-sasl-login-xx.txt \
	draft-newman-sasl-c-api-xx.txt rfc1321.txt rfc1939.txt rfc2104.txt \
	rfc2195.txt rfc2222.txt rfc2243.txt rfc2245.txt rfc2289.txt \
	rfc2444.txt rfc2595.txt rfc2831.txt rfc2945.txt rfc3174.txt \
	server-plugin-flow.fig testing.txt

HTDOCS=	advanced appconvert components gssapi index install macosx \
	mechanisms options plugprog programming readme sysadmin upgrading \
	windows

.include "${.CURDIR}/../../security/cyrus-sasl2/Makefile.common"
