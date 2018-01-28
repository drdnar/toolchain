#----------------------------
# Makefile
#----------------------------

# common/os specific things
ifeq ($(OS),Windows_NT)
SHELL      =cmd.exe
NATIVEPATH =$(subst /,\,$(1))
WINPATH    =$(NATIVEPATH)
CP         =xcopy /y
PREFIX    ?=C:
WINCHKPATH =$(NATIVEPATH)
WINCHKDIR :=if exist
RMDIR      =rmdir /s /q
else
NATIVEPATH =$(subst \,/,$(1))
WINPATH    =$(subst \,\\,$(shell winepath --windows $(1)))
CP         =cp
PREFIX    ?=$(HOME)
RMDIR      =rm -rf
endif

DEV        ?=$(call NATIVEPATH,$(PREFIX)/CEdev)
BIN        ?=$(call NATIVEPATH,$(DEV)/bin)

INSTALLLOC :=$(call NATIVEPATH,$(DESTDIR)$(DEV))
I_LOC      :=$(call NATIVEPATH,$(INSTALLLOC)/lib)

CSTARTUP_SRC  :=cstartup.src
CCLEANUP_SRC  :=ccleanup.src
LIBHEADER_SRC :=libheader.src

all:

clean:

install:
	$(CP) $(CSTARTUP_SRC) $(I_LOC)
	$(CP) $(CCLEANUP_SRC) $(I_LOC)
	$(CP) $(LIBHEADER_SRC) $(I_LOC)

uninstall:
	$(WINCHKDIR) $(call WINCHKPATH,$(I_LOC)) $(RMDIR) $(I_LOC)

.PHONY: all clean install uninstall