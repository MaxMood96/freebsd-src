.include <src.opts.mk>

PACKAGE=	toolchain
PROG_CXX=	llvm-nm

SRCDIR=		llvm/tools/llvm-nm
SRCS+=		llvm-nm-driver.cpp
SRCS+=		llvm-nm.cpp

.include "${SRCTOP}/lib/clang/llvm.pre.mk"

CFLAGS+=	-I${.OBJDIR}

INCFILE=	Opts.inc
TDFILE=		${LLVM_BASE}/${SRCDIR}/Opts.td
GENOPT=		-gen-opt-parser-defs
${INCFILE}: ${TDFILE}
	${LLVM_TBLGEN} ${GENOPT} -I ${LLVM_SRCS}/include -d ${.TARGET:C/$/.d/} \
	    -o ${.TARGET} ${TDFILE}
TGHDRS+=	${INCFILE}

DEPENDFILES+=	${TGHDRS:C/$/.d/}
DPSRCS+=	${TGHDRS}
CLEANFILES+=	${TGHDRS} ${TGHDRS:C/$/.d/}

.if ${MK_LLVM_BINUTILS} != "no"
LINKS+=		${BINDIR}/llvm-nm ${BINDIR}/nm
MLINKS+=	llvm-nm.1 nm.1
.endif

.include "../llvm.prog.mk"
