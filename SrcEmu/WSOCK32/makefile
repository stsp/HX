OWDIR = $(WATCOM)
NAME = wsock32

ifneq ($(DEBUG),)
OUTDIR=DEBUG
COPTD=-D_DEBUG
#WTLIB=$(WATT32)/lib/wattcpwd.lib
WTLIB=$(WATT32)/lib/wattcpwf.lib
else
OUTDIR=RELEASE
COPTD=
WTLIB=libcsock.lib
endif

CC = wcc386
CFLAGS = -mf -3r -zq -bt=dos -bm -bd -ox -Iinclude $(COPTD)
#CC=wcc386.exe -mf -w6 -3r -zq -bt=nt -bm -bd -ox -I$(WATT32)/inc -fo=$* $(COPTD)
LINK=wlink
LIBRARY = lib $(WTLIB)

ALL: $(OUTDIR) $(OUTDIR)/$(NAME).DLL

$(OUTDIR):
	@mkdir $(OUTDIR)

$(OUTDIR)/$(NAME).DLL: $(OUTDIR)/$(NAME).OBJ $(WTLIB) $(NAME).rsp a.lnk
	$(LINK) format windows pe dll name $*.DLL op quiet, eliminate, map=$@, implib=$@ @a.lnk

a.lnk:
	echo file $(OUTDIR)/$(NAME).OBJ >>$@
	echo libpath $(OWDIR)/lib386/nt >>$@
	echo libpath $(OWDIR)/lib386 >>$@
	echo library clib3r.lib >>$@
	echo library $(LIBOMF)/hxowdll.lib >>$@
	echo library $(LIBCOFF)/dkrnl32.lib >>$@
ifneq ($(DEBUG),)
	echo library $(LIBCOFF)/duser32.lib >>$@
endif
	echo $(LIBRARY) >>$@
	echo @$(NAME).rsp >>$@

$(OUTDIR)/$(NAME).OBJ: $(NAME).c makefile version.h
	$(CC) $(CFLAGS) -fo=$@ $(NAME).c

clean:
	@$(RM) $(OUTDIR)/*.obj
	@$(RM) $(OUTDIR)/*.dll
	@$(RM) $(OUTDIR)/*.lib
	@$(RM) $(OUTDIR)/*.lst
