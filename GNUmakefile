PROG=	opunra
MAN=	opunra.1 opunra.conf.5

SRCS=	parse.y opunra.c env.c

include config.mk

override CFLAGS:=-I. -Ilibopenbsd -O2 -Wall -Wextra ${OS_CFLAGS} ${CFLAGS}

all: ${PROG}

OBJS:=	${SRCS:.y=.c}
OBJS:=	${OBJS:.c=.o}

${PROG}: ${OBJS}
	${CC} ${CFLAGS} $^ -o $@ ${LDFLAGS} ${LDLIBS}

install: ${PROG} ${MAN}
	mkdir -p -m 0755 ${DESTDIR}${BINDIR}
	mkdir -p -m 0755 ${DESTDIR}${MANDIR}/man1
	mkdir -p -m 0755 ${DESTDIR}${MANDIR}/man5
	cp -f ${PROG} ${DESTDIR}${BINDIR}
	chown ${BINOWN}:${BINGRP} ${DESTDIR}${BINDIR}/${PROG}
	chmod ${BINMODE} ${DESTDIR}${BINDIR}/${PROG}
	cp -f opunra.1 ${DESTDIR}${MANDIR}/man1
	cp -f opunra.conf.5 ${DESTDIR}${MANDIR}/man5

uninstall:
	rm -f ${DESTDIR}${BINDIR}/${PROG}
	rm -f ${DESTDIR}${PAMDIR}/opunra
	rm -f ${DESTDIR}${MANDIR}/man1/opunra.1
	rm -f ${DESTDIR}${MANDIR}/man5/opunra.conf.5

clean:
	rm -f ${PROG} ${OBJS} ${OBJS:.o=.d} parse.c

-include ${OBJS:.o=.d}

.PHONY: all clean install uninstall
