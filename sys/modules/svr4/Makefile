# $FreeBSD$

.PATH:	${.CURDIR}/../../${MACHINE_CPUARCH}/svr4 ${.CURDIR}/../../compat/svr4
KMOD=	svr4
SRCS=	svr4_sysent.c svr4_sysvec.c opt_compat.h opt_svr4.h \
	vnode_if.h imgact_svr4.c svr4_signal.c svr4_fcntl.c \
	svr4_misc.c svr4_ioctl.c svr4_stat.c svr4_filio.c \
	svr4_termios.c svr4_stream.c svr4_socket.c svr4_sockio.c \
	svr4_machdep.c svr4_resource.c svr4_ipc.c
OBJS=	svr4_locore.o 
EXPORT_SYMS= svr4_delete_socket

SRCS+=	opt_ktrace.h opt_sysvipc.h

CLEANFILES=	svr4_assym.h svr4_genassym.o

svr4_assym.h: svr4_genassym.o
	sh ${SYSDIR}/kern/genassym.sh svr4_genassym.o > ${.TARGET}

svr4_locore.o: svr4_locore.s svr4_assym.h
	${CC} -c -x assembler-with-cpp -DLOCORE ${CFLAGS} \
		${.IMPSRC} -o ${.TARGET}

svr4_genassym.o: svr4_genassym.c svr4.h
	${CC} -c ${CFLAGS:N-fno-common} ${.IMPSRC}

.if !defined(KERNBUILDDIR) && defined(DEBUG)
opt_svr4.h:
	echo "#define DEBUG_SVR4 1" > ${.TARGET}
.endif

.include <bsd.kmod.mk>
