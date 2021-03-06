## Process this file with automake to produce Makefile.in

SUBDIRS = advisors generator scripting

srvbin = freeciv-server

bin_PROGRAMS = $(srvbin)
lib_LTLIBRARIES = libfreeciv-srv.la
AM_CPPFLAGS = \
	-I$(top_srcdir)/ai \
	-I$(top_srcdir)/ai/classic \
	-I$(top_srcdir)/common \
	-I$(top_srcdir)/common/aicore \
	-I$(top_srcdir)/common/scriptcore \
	-I$(top_srcdir)/utility \
	-I$(srcdir)/advisors \
	-I$(srcdir)/generator \
	-I$(srcdir)/scripting \
	$(LIBGGZ_INCLUDES) $(GGZDMOD_INCLUDES) \
	$(FCDB_MYSQL_CFLAGS) $(FCDB_POSTGRES_CFLAGS) $(FCDB_SQLITE3_CFLAGS)

if MINGW32
SERVERICON=../win32/servericon.o
endif

exe_sources = \
		civserver.c	\
		civserver.h

libfreeciv_srv_la_SOURCES = \
		aiiface.c	\
		aiiface.h	\
		auth.c		\
		auth.h		\
		barbarian.c	\
		barbarian.h	\
		citizenshand.c	\
		citizenshand.h	\
		cityhand.c	\
		cityhand.h	\
		citytools.c	\
		citytools.h	\
		cityturn.c	\
		cityturn.h	\
		commands.c	\
		commands.h	\
		connecthand.c	\
		connecthand.h	\
		console.c	\
		console.h	\
		diplhand.c	\
		diplhand.h	\
		diplomats.c	\
		diplomats.h	\
		edithand.c	\
		edithand.h	\
		fcdb.c		\
		fcdb.h		\
		gamehand.c	\
		gamehand.h	\
		ggzserver.c	\
		ggzserver.h	\
		handchat.c	\
		handchat.h	\
		hand_gen.h	\
		hand_gen.c	\
		maphand.c	\
		maphand.h	\
		meta.c		\
		meta.h		\
		notify.c	\
		notify.h	\
		plrhand.c	\
		plrhand.h	\
		report.c	\
		report.h	\
		rssanity.c	\
		rssanity.h	\
		ruleset.c	\
		ruleset.h	\
		sanitycheck.c	\
		sanitycheck.h	\
		savegame.c	\
		savegame.h	\
		savegame2.c	\
		savegame2.h	\
		score.c		\
		score.h		\
		sernet.c	\
		sernet.h	\
		settings.c	\
		settings.h	\
		spacerace.c	\
		spacerace.h	\
		srv_log.c	\
		srv_log.h	\
		srv_main.c	\
		srv_main.h	\
		stdinhand.c	\
		stdinhand.h	\
		techtools.h	\
		techtools.c	\
		unithand.c	\
		unithand.h	\
		unittools.c	\
		unittools.h	\
		voting.c	\
		voting.h

# hand_gen.c & hand_gen.h are generated files, but as they are generated
# outside this directory (when building common) there's no point in
# setting them to BUILT_SOURCES.

da_libs = 

if AI_MOD_DEFAULT_NEEDED
da_libs += $(top_builddir)/ai/default/libdefaultai.la
endif

if AI_MOD_STATIC_CLASSIC
da_libs += $(top_builddir)/ai/classic/libclassicai.la
endif
if AI_MOD_STATIC_THREADED
da_libs += $(top_builddir)/ai/threaded/libthreadedai.la
endif

# These files are not generated to builddir, but to srcdir */
MAINTAINERCLEANFILES = \
	$(srcdir)/hand_gen.c \
	$(srcdir)/hand_gen.h

srvlibs = \
 $(da_libs) \
 $(top_builddir)/ai/libaicommon.la \
 $(top_builddir)/server/advisors/libadvisors.la \
 $(top_builddir)/server/generator/libgenerator.la \
 $(top_builddir)/server/scripting/libscripting_fcdb.la \
 $(top_builddir)/server/scripting/libscripting_server.la

libfreeciv_srv_la_LIBADD = \
 $(srvlibs) $(SRV_LIB_LIBS) \
 $(LUA_LIBS) $(TOLUA_LIBS) $(LUASQL_LIBS)

exe_ldflags = $(GGZDMOD_LDFLAGS)

exe_ldadd = \
 ./libfreeciv-srv.la \
 $(top_builddir)/common/libfreeciv.la \
 $(INTLLIBS) \
 $(MAPIMG_WAND_LIBS) \
 $(SERVER_LIBS) $(LIB_GGZDMOD) $(SERVERICON)

freeciv_server_SOURCES = $(exe_sources)
freeciv_server_LDFLAGS = $(exe_ldflags)
freeciv_server_LDADD = $(exe_ldadd)

desktopfiledir = @DESKTOPDIR@
desktopfile_DATA = \
	freeciv-server.desktop

appdatafiledir = @APPDATADIR@
appdatafile_DATA = \
	freeciv-server.appdata.xml
