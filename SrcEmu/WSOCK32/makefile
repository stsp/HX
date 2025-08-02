OWDIR = $(WATCOM)
NAME = wsock32
LIBOMF = .
LIBCOFF = .
OUTDIR=RELEASE
COPTD=
WTLIB=w32/libcsock.lib

CC = wcc386
CFLAGS = -mf -3r -zq -bt=dos -bm -bd -ox -Iinclude $(COPTD)
#CC=wcc386.exe -mf -w6 -3r -zq -bt=nt -bm -bd -ox -I$(WATT32)/inc -fo=$* $(COPTD)
LINK=wlink
LIBRARY = lib $(WTLIB)

all: $(OUTDIR) $(OUTDIR)/$(NAME).dll

$(OUTDIR):
	@mkdir $(OUTDIR)

$(OUTDIR)/$(NAME).dll: $(OUTDIR)/$(NAME).obj $(WTLIB) $(NAME).rsp a.lnk
	$(LINK) format windows pe dll name $@ op quiet, eliminate, map=$(dir $@)$(NAME).map, implib=$(dir $@)$(NAME).imp @a.lnk
	chmod -x $@

a.lnk:
	echo file $(OUTDIR)/$(NAME).obj >$@
	echo libpath $(OWDIR)/lib386/nt >>$@
	echo library $(LIBCOFF)/DKRNL32.LIB >>$@
ifneq ($(DEBUG),)
	echo library $(LIBCOFF)/duser32.lib >>$@
endif
	echo $(LIBRARY) >>$@
	echo @$(NAME).rsp >>$@

$(OUTDIR)/$(NAME).obj: $(NAME).c makefile version.h
	$(CC) $(CFLAGS) -fo=$@ $(NAME).c

clean:
	$(RM) $(OUTDIR)/*.obj
	$(RM) $(OUTDIR)/*.dll
	$(RM) $(OUTDIR)/*.lib
	$(RM) $(OUTDIR)/*.lst
	$(RM) a.lnk
