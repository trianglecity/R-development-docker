#
# ${R_HOME}/src/modules/X11/Makefile


srcdir = .
top_srcdir = ../../..

top_builddir = ../../..
subdir = src/modules/X11
R_HOME = $(top_builddir)

include $(top_builddir)/Makeconf

## When compiling rbitmap.c it is essential that we find the
## png.h matching BITMAP_LIBS.  Since /opt/X11 on macOS contains libpng
## and we might want our own version, we give priority to BITMAP_*
ALL_CPPFLAGS =  -I/usr/include/libpng12 -I/usr/include/x86_64-linux-gnu $(R_XTRA_CPPFLAGS) $(X_CFLAGS) -I/usr/include/pango-1.0 -I/usr/include/harfbuzz -I/usr/include/pango-1.0 -I/usr/include/cairo -I/usr/include/glib-2.0 -I/usr/lib/x86_64-linux-gnu/glib-2.0/include -I/usr/include/pixman-1 -I/usr/include/freetype2 -I/usr/include/libpng12 \
  -I$(top_srcdir)/src/library/grDevices/src/cairo $(CPPFLAGS) $(DEFS)
ALL_CFLAGS = $(ALL_CFLAGS_LO)
ALL_X_LIBS = $(X_PRE_LIBS) -lpangocairo-1.0 -lpango-1.0 -lgobject-2.0 -lglib-2.0 -lpng12 -lz -lcairo -lX11 -lXext $(X_LIBS) $(X_EXTRA_LIBS)

SOURCES = devX11.c rotated.c rbitmap.c 
DEPENDS = $(SOURCES:.c=.d)
OBJECTS = $(SOURCES:.c=.o)
DE_SOURCES = dataentry.c
DE_OBJECTS = $(DE_SOURCES:.c=.o)
HEADERS = bitmap.h devX11.h rotated.h rlogo_icon.h

distdir = $(top_builddir)/$(PACKAGE)-$(VERSION)/$(subdir)
DISTFILES = \
	Makefile.in $(SOURCES) $(HEADERS) $(DE_SOURCES)

R_X11_la = R_X11$(SHLIB_EXT)
## Note that this is used after LDFLAGS, which usually contains -L flags.
## AIX needs LIBM
R_X11_la_LIBADD = -ltiff -ljpeg -lpng12 $(ALL_X_LIBS) $(LIBR1) $(LIBM) # $(LIBINTL)

R_de_la = R_de$(SHLIB_EXT)
R_de_la_LIBADD = $(ALL_X_LIBS) $(LIBR1) $(LIBM) # $(LIBINTL)

all: R

Makefile: $(srcdir)/Makefile.in \
  $(top_builddir)/config.status \
  $(SOURCES)
	@cd $(top_builddir) && $(SHELL) ./config.status $(subdir)/$@

Makedeps: Makefile $(DEPENDS)
	@cat $(DEPENDS) >> Makefile
	@touch $@

R: Makedeps
	@$(MAKE) $(R_X11_la) $(R_de_la)
	@$(MAKE) rhome="$(abs_top_builddir)" install

$(R_X11_la): $(OBJECTS)
	$(SHLIB_LINK) -o $@ $(OBJECTS) $(R_X11_la_LIBADD)

$(R_de_la): $(DE_OBJECTS)
	$(SHLIB_LINK) -o $@ $(DE_OBJECTS) $(R_de_la_LIBADD)

install: installdirs
	@$(SHELL) $(top_srcdir)/tools/copy-if-change $(R_X11_la) "$(DESTDIR)$(Rexecmodulesdir)/$(R_X11_la)"
	@$(SHELL) $(top_srcdir)/tools/copy-if-change $(R_de_la) "$(DESTDIR)$(Rexecmodulesdir)/$(R_de_la)"
installdirs:
	@$(MKINSTALLDIRS) "$(DESTDIR)$(Rexecmodulesdir)"
install-strip: installdirs
	@$(SHELL) $(top_srcdir)/tools/copy-if-change $(R_X11_la) "$(DESTDIR)$(Rexecmodulesdir)/$(R_X11_la)"
	@$(SHELL) $(top_srcdir)/tools/copy-if-change $(R_X11_la) "$(DESTDIR)$(Rexecmodulesdir)/$(R_de_la)"
	@if test -n "$(STRIP_LIBS)"; then \
	  $(STRIP_LIBS) "$(DESTDIR)$(Rexecmodulesdir)/$(R_X11_la)" ;\
	  $(STRIP_LIBS) "$(DESTDIR)$(Rexecmodulesdir)/$(R_de_la)" ;\
	fi
uninstall:
	@rm -f "$(Rexecmodulesdir)/R_X11$(SHLIB_EXT)"\
	  "$(Rexecmodulesdir)/R_de(SHLIB_EXT)"

mostlyclean: clean
clean:
	@-rm -rf .libs _libs
	@-rm -f Makedeps *.d *.o *.a *.lo *.la *$(SHLIB_EXT)
distclean: clean
	@-rm -f Makefile
maintainer-clean: distclean

TAGS info dvi check:

distdir: $(DISTFILES)
	@for f in $(DISTFILES); do \
	  test -f $(distdir)/$${f} \
	    || ln $(srcdir)/$${f} $(distdir)/$${f} 2>/dev/null \
	    || cp -p $(srcdir)/$${f} $(distdir)/$${f}; \
	done

## Automagically generated dependencies:

devX11.o: devX11.c ../../../src/include/config.h \
 ../../../src/include/Defn.h ../../../src/include/R_ext/Complex.h \
 ../../../src/include/Rinternals.h ../../../src/include/R_ext/Arith.h \
 ../../../src/include/R_ext/libextern.h \
 ../../../src/include/R_ext/Boolean.h ../../../src/include/R_ext/Error.h \
 ../../../src/include/R_ext/Memory.h ../../../src/include/R_ext/Utils.h \
 ../../../src/include/R_ext/Print.h ../../../src/include/Rinlinedfuns.h \
 ../../../src/include/Errormsg.h \
 ../../../src/include/R_ext/GraphicsEngine.h \
 ../../../src/include/R_ext/GraphicsDevice.h \
 ../../../src/include/Fileio.h rotated.h \
 ../../../src/include/R_ext/eventloop.h devX11.h \
 /usr/include/cairo/cairo.h /usr/include/cairo/cairo-version.h \
 /usr/include/cairo/cairo-features.h \
 /usr/include/cairo/cairo-deprecated.h /usr/include/cairo/cairo-xlib.h \
 /usr/include/cairo/cairo.h rlogo_icon.h \
 ../../../src/include/Rmodules/RX11.h ../../../src/include/Rconnections.h \
 ../../../src/include/R_ext/Connections.h \
 ../../../src/library/grDevices/src/cairo/cairoFns.c bitmap.h \
 ../../../src/include/R_ext/Rdynload.h
rotated.o: rotated.c ../../../src/include/config.h rotated.h
rbitmap.o: rbitmap.c ../../../src/include/config.h bitmap.h \
 /usr/include/libpng12/png.h /usr/include/libpng12/pngconf.h \
 ../../../src/include/R_ext/Error.h
