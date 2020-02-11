SRCS=		luamotif.c widgets.c constants.c
LIB=		motif

LUAVER=		$(shell lua -v 2>&1 | cut -c 5-7)

CFLAGS+=	-Wall -O3 -fPIC -I/usr/include -I${PKGDIR}/include \
                $(shell lua-config --include 2>/dev/null || pkg-config --cflags lua50)
LDADD+=		-L${XDIR}/lib -L${PKGDIR}/lib -lXm -lXt -lX11 -lbsd

PKGDIR=		/usr
LIBDIR=		${PKGDIR}/lib
LUADIR=		${LIBDIR}/lua/${LUAVER}

${LIB}.so:	${SRCS:.c=.o}
	$(CC) -shared -o ${LIB}.so ${CFLAGS} ${SRCS:.c=.o} ${LDADD}

.PHONY: clean
clean:
	$(RM) $(wildcard *.o *.so)

.PHONY: install
install:
	-mkdir -p ${DESTDIR}${LUADIR}
	install -m 755 ${LIB}.so ${DESTDIR}${LUADIR}/${LIB}.so
