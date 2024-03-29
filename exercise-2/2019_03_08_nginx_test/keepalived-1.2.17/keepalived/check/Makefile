
# Makefile
#
# Keepalived OpenSource project.
#
# Copyright (C) 2001-2012 Alexandre Cassen, <acassen@gmail.com>

CC	 = gcc
SNMP_FLAG = _WITHOUT_SNMP_
INCLUDES = -I../include -I../../lib
CFLAGS	 = $(INCLUDES) -g -O2  -I/usr/src/linux/include -I/usr/src/linux/include \
	   -Wall -Wunused -Wstrict-prototypes
DEFS	 = -D_KRNL_2_6_ -D_WITH_LVS_ -D_HAVE_IPVS_SYNCD_ -D_WITH_VRRP_ -D_WITHOUT_SNMP_ -D_WITH_SO_MARK_ 
COMPILE	 = $(CC) $(CFLAGS) $(DEFS)

OBJS = 	check_daemon.o check_data.o check_parser.o \
	check_api.o check_tcp.o check_http.o check_ssl.o \
	check_smtp.o check_misc.o ipwrapper.o ipvswrapper.o
ifeq ($(SNMP_FLAG),_WITH_SNMP_)
  OBJS += check_snmp.o
endif

HEADERS = $(OBJS:.o=.h)

.c.o:
	$(COMPILE) -c $<

all:	$(OBJS)

clean:
	rm -f *.a *.o *~

distclean: clean
	rm -f Makefile

check_daemon.o: check_daemon.c ../include/check_daemon.h \
  ../include/check_parser.h ../include/check_data.h ../include/check_api.h \
  ../include/global_data.h ../include/ipwrapper.h ../include/ipwrapper.h \
  ../include/pidfile.h ../include/daemon.h ../../lib/list.h ../../lib/memory.h \
  ../../lib/parser.h ../../lib/signals.h ../../lib/bitops.h ../include/vrrp_netlink.h \
  ../include/vrrp_if.h ../include/snmp.h ../include/check_snmp.h
check_data.o: check_data.c ../include/check_data.h \
  ../include/check_api.h ../../lib/memory.h ../../lib/utils.h
check_parser.o: check_parser.c ../include/check_parser.h \
  ../include/check_data.h ../include/check_api.h ../include/global_data.h \
  ../include/global_parser.h ../../lib/parser.h ../../lib/memory.h \
  ../../lib/utils.h
check_api.o: check_api.c ../include/check_api.h ../../lib/parser.h \
  ../../lib/memory.h ../../lib/utils.h ../../lib/bitops.h ../include/check_misc.h \
  ../include/check_tcp.h ../include/check_http.h ../include/check_ssl.h
check_tcp.o: check_tcp.c ../include/check_tcp.h ../include/check_api.h \
  ../../lib/memory.h ../include/ipwrapper.h ../include/layer4.h \
  ../include/smtp.h ../../lib/utils.h ../../lib/parser.h
check_http.o: check_http.c ../include/check_http.h ../include/check_ssl.h \
  ../include/check_api.h ../../lib/memory.h ../../lib/parser.h \
  ../../lib/utils.h
check_ssl.o: check_ssl.c ../include/check_ssl.h ../include/check_api.h \
  ../../lib/memory.h ../../lib/parser.h ../include/smtp.h \
  ../../lib/utils.h
check_smtp.o: check_smtp.c ../include/check_smtp.h ../include/check_api.h \
  ../../lib/memory.h ../include/ipwrapper.h ../include/smtp.h \
  ../../lib/utils.h ../../lib/notify.h ../../lib/parser.h ../include/daemon.h
check_misc.o: check_misc.c ../include/check_misc.h ../include/check_api.h \
  ../../lib/memory.h ../include/ipwrapper.h ../include/smtp.h \
  ../../lib/utils.h ../../lib/notify.h ../../lib/parser.h ../include/daemon.h
ipwrapper.o: ipwrapper.c ../include/ipwrapper.h ../../lib/memory.h \
  ../../lib/utils.h ../../lib/notify.h ../include/snmp.h ../include/check_snmp.h
ipvswrapper.o: ipvswrapper.c ../include/ipvswrapper.h ../../lib/utils.h \
  ../../lib/memory.h
check_snmp.o: check_snmp.c ../include/check_snmp.h ../include/check_data.h \
  ../../lib/list.h ../include/ipvswrapper.h ../include/ipwrapper.h ../include/global_data.h
