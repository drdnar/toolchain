#----------------------------
# Makefile
#----------------------------

# common/os specific things
ifeq ($(OS),Windows_NT)
SHELL      =cmd.exe
NATIVEPATH =$(subst /,\,$(1))
RM         =del /f 2>nul
CP         =echo f|xcopy /y
PREFIX    ?=C:
NAME       =fasmg.exe
FASMGP     =windows\$(NAME)
else
NAME       =fasmg
ifeq ($(shell uname -s),Darwin)
FASMGP     =macos/$(NAME)
else
FASMGP     =linux/$(NAME)
endif
NATIVEPATH =$(subst \,/,$(1))
RM         =rm -f
CP         =cp
PREFIX    ?=$(HOME)
ADDEXE     =&& chmod +x $(NAME)
endif

DEV ?=$(call NATIVEPATH,$(PREFIX)/CEdev)
BIN ?=$(call NATIVEPATH,$(DEV)/bin)
INC ?=$(call NATIVEPATH,$(DEV)/include/fasmg-ez80/)

INSTALLLOC :=$(call NATIVEPATH,$(DESTDIR)$(DEV))

INCDIR     :=$(call NATIVEPATH,../../src/include/)
FILES      :=$(addprefix $(INCDIR),ez80.inc ld.fasmg ti84pceg.inc tiformat.inc)
INCFILES   :=$(addprefix $(INC),ez80.inc ld.fasmg ti84pceg.inc tiformat.inc)

all: $(FILES)
	$(CP) $(call NATIVEPATH,$(FASMGP)) . $(ADDEXE)

$(FILES):
	$(CP) $(call NATIVEPATH,fasmg-ez80/$(@F)) $(INCDIR)$(@F)

clean:
	$(RM) $(FILES)
	$(RM) $(NAME)

install: $(INCFILES)
	$(CP) $(NAME) $(BIN)

$(INCFILES):
	$(CP) $(call NATIVEPATH,fasmg-ez80/$(@F)) $(INC)$(@F)

uninstall:

.PHONY: all clean install uninstall $(FILES)
