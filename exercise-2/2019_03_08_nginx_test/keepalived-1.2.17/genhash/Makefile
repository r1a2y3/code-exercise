# Makefile.in
#
# Copyright (C) 2001-2012 Alexandre Cassen, <acassen@gmail.com>

EXEC = genhash
BIN  = ../bin

prefix      = /usr/keepalived-1.2.17
exec_prefix = ${prefix}
bindir      = ${exec_prefix}/bin
mandir      = ${datarootdir}/man
datarootdir = ${prefix}/share

CC = gcc
STRIP = strip
INCLUDES = -I../lib
CFLAGS = $(INCLUDES) -g -O2 -D_WITH_SO_MARK_  -I/usr/src/linux/include -I/usr/src/linux/include \
	 -Wall -Wunused -Wstrict-prototypes
LDFLAGS = -lssl -lcrypto -lcrypt  

OBJS = main.o sock.o layer4.o http.o ssl.o
LIB_OBJS = ../lib/timer.o ../lib/scheduler.o ../lib/memory.o ../lib/list.o \
	   ../lib/utils.o ../lib/html.o ../lib/signals.o ../lib/logger.o

all:	$(BIN)/$(EXEC)
	$(STRIP) $(BIN)/$(EXEC)
	@echo ""
	@echo "Make complete"

$(BIN)/$(EXEC): $(LIB_OBJS) $(OBJS)
	@set -e; \
	echo "Building $(BIN)/$(EXEC)" && \
	$(CC) -o $(BIN)/$(EXEC) $(LIB_OBJS) $(OBJS) $(LDFLAGS)

clean:
	rm -f core *.o

distclean: clean
	rm -f Makefile $(BIN)/$(EXEC)

uninstall:
	rm -f $(DESTDIR)$(bindir)/$(EXEC)
	rm -f $(DESTDIR)$(mandir)/man1/genhash.1

install:
	install -d $(DESTDIR)$(bindir)
	install -m 755 $(BIN)/$(EXEC) $(DESTDIR)$(bindir)/
	install -d $(DESTDIR)$(mandir)/man1
	install -m 644 ../doc/man/man1/genhash.1 $(DESTDIR)$(mandir)/man1

mrproper: clean distclean
	rm -f config.*

# Code dependencies

main.o: main.c include/main.h ../lib/utils.h include/sock.h ../lib/timer.h \
	include/http.h include/ssl.h ../lib/scheduler.h ../lib/memory.h
sock.o: sock.c include/sock.h ../lib/utils.h include/layer4.h include/ssl.h include/main.h \
	../lib/memory.h
layer4.o: layer4.c include/layer4.h ../lib/scheduler.h ../lib/utils.h \
	include/main.h include/ssl.h
http.o: http.c include/http.h include/sock.h ../lib/scheduler.h ../lib/utils.h \
	include/layer4.h include/main.h ../lib/html.h ../lib/timer.h ../lib/scheduler.h \
	../lib/memory.h
ssl.o: ssl.c include/ssl.h include/http.h include/main.h ../lib/utils.h ../lib/html.h
