# st - simple terminal
# See LICENSE file for copyright and license details.
.POSIX:

include config.mk

SRC = st.c x.c
OBJ = $(SRC:.c=.o)

all: options st

options:
	@echo st build options:
	@echo "CFLAGS  = $(STCFLAGS)"
	@echo "LDFLAGS = $(STLDFLAGS)"
	@echo "CC      = $(CC)"

config.h:
	cp config.def.h config.h

.c.o:
	$(CC) $(STCFLAGS) -c $<

st.o: config.h st.h win.h
x.o: arg.h config.h st.h win.h

$(OBJ): config.h config.mk

st: $(OBJ)
	$(CC) $(OBJ) $(STCFLAGS) $(STLDFLAGS) -o $@

patch:
	patch -i st-scrollback-20210507-4536f46.diff
	patch -i st-scrollback-mouse-20191024-a2c479c.diff
	patch -i st-scrollback-mouse-altscreen-20200416-5703aa0.diff
	patch -i st-scrollback-mouse-selection-20220111.diff
	patch -i st-ligatures-scrollback-20210824-0.8.4.diff
	patch -i st-gtkthemevariant-20220110.diff
	patch -i st-colortheme-20220110.diff
	patch -i st-firacode-20220110.diff

clean:
	rm -f st $(OBJ) st-$(VERSION).tar.gz

dist: clean
	mkdir -p st-$(VERSION)
	cp -R FAQ LEGACY TODO LICENSE Makefile README config.mk\
		config.def.h st.info st.1 arg.h st.h win.h $(SRC)\
		st-$(VERSION)
	tar -cf - st-$(VERSION) | gzip > st-$(VERSION).tar.gz
	rm -rf st-$(VERSION)

install: st
	mkdir -p $(DESTDIR)$(PREFIX)/bin
	cp -f st $(DESTDIR)$(PREFIX)/bin
	chmod 755 $(DESTDIR)$(PREFIX)/bin/st
	mkdir -p $(DESTDIR)$(MANPREFIX)/man1
	sed "s/VERSION/$(VERSION)/g" < st.1 > $(DESTDIR)$(MANPREFIX)/man1/st.1
	chmod 644 $(DESTDIR)$(MANPREFIX)/man1/st.1
	tic -sx st.info
	mkdir -p $(DESTDIR)/usr/share/applications
	cp -f st.desktop $(DESTDIR)/usr/share/applications/st.desktop
	mkdir -p $(DESTDIR)/usr/share/icons/hicolor/scalable/apps
	cp -f st-terminal.svg $(DESTDIR)/usr/share/icons/hicolor/scalable/apps/st-terminal.svg
	mkdir -p $(DESTDIR)/usr/share/icons/hicolor/symbolic/apps
	cp -f st-terminal-symbolic.svg $(DESTDIR)/usr/share/icons/hicolor/symbolic/apps/st-terminal-symbolic.svg
	@echo Please see the README file regarding the terminfo entry of st.

uninstall:
	rm -f $(DESTDIR)$(PREFIX)/bin/st
	rm -f $(DESTDIR)$(MANPREFIX)/man1/st.1

.PHONY: all options clean dist install uninstall
