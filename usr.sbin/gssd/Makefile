# $FreeBSD$

.include <src.opts.mk>

PROG=	gssd
MAN=	gssd.8
SRCS=	gssd.c gssd.h gssd_svc.c gssd_xdr.c gssd_prot.c

CFLAGS+= -I. -I/usr/local/include
LDFLAGS+=-L/usr/local/lib
LDADD+= /usr/local/lib/libgssapi_krb5.so /usr/local/lib/libkrb5.so /usr/local/lib/libk5crypto.so /usr/local/lib/libcom_err.so
WARNS?= 1

#LIBADD=	gssapi
#.if ${MK_KERBEROS_SUPPORT} != "no"
#LIBADD+=	krb5 roken
#.else
#CFLAGS+= -DWITHOUT_KERBEROS
#.endif

CLEANFILES= gssd_svc.c gssd_xdr.c gssd.h

RPCSRC=	${SRCTOP}/sys/kgssapi/gssd.x
RPCGEN= RPCGEN_CPP=${CPP:Q} rpcgen -L -C -M

gssd_svc.c: ${RPCSRC} gssd.h
	${RPCGEN} -m -o ${.TARGET} ${RPCSRC}

gssd_xdr.c: ${RPCSRC} gssd.h
	${RPCGEN} -c -o ${.TARGET} ${RPCSRC}

gssd.h: ${RPCSRC}
	${RPCGEN} -h -o ${.TARGET} ${RPCSRC}

.PATH:	${SRCTOP}/sys/kgssapi

.include <bsd.prog.mk>
