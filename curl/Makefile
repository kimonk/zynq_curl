ifndef PETALINUX
$(error "Error: PETALINUX environment variable not set.  Change to the root of your PetaLinux install, and source the settings.sh file")
endif

include apps.common.mk

APP = curl

# Add any other object files to this list below
#APP_OBJS = ./src/tool_main.o 
APP_OBJS = ./src/tool_binmode.o ./src/slist_wc.o ./src/tool_binmode.o ./src/tool_bname.o ./src/tool_cb_dbg.o ./src/tool_cb_prg.o ./src/tool_cb_rea.o ./src/tool_cb_see.o ./src/tool_cb_hdr.o ./src/tool_cb_wrt.o ./src/tool_cfgable.o ./src/tool_convert.o ./src/tool_dirhie.o ./src/tool_doswin.o ./src/tool_easysrc.o ./src/tool_formparse.o ./src/tool_getparam.o ./src/tool_getpass.o ./src/tool_help.o ./src/tool_helpers.o ./src/tool_homedir.o ./src/tool_hugehelp.o ./src/tool_libinfo.o ./src/tool_metalink.o ./src/tool_mfiles.o ./src/tool_msgs.o ./src/tool_operate.o ./src/tool_operhlp.o ./src/tool_panykey.o ./src/tool_paramhlp.o ./src/tool_parsecfg.o ./src/tool_setopt.o ./src/tool_sleep.o ./src/tool_strdup.o ./src/tool_urlglob.o ./src/tool_util.o ./src/tool_vms.o ./src/tool_writeenv.o ./src/tool_writeout.o ./src/tool_xattr.o ./src/tool_main.o

#APP_OBJS = ./src/tool_main.o ./src/slist_wc.o ./src/tool_binmode.o ./src/tool_bname.o ./src/tool_cb_dbg.o ./src/tool_cb_prg.o ./src/tool_cb_rea.o ./src/tool_cb_see.o ./src/tool_cb_hdr.o ./src/tool_cb_wrt.o ./src/tool_cfgable.o ./src/tool_convert.o ./src/tool_dirhie.o ./src/tool_doswin.o ./src/tool_easysrc.o ./src/tool_formparse.o ./src/tool_getparam.o ./src/tool_getpass.o ./src/tool_help.o ./src/tool_helpers.o ./src/tool_homedir.o ./src/tool_hugehelp.o ./src/tool_libinfo.o ./src/tool_metalink.o ./src/tool_mfiles.o ./src/tool_msgs.o ./src/tool_operate.o ./src/tool_operhlp.o ./src/tool_panykey.o ./src/tool_paramhlp.o ./src/tool_parsecfg.o ./src/tool_setopt.o ./src/tool_sleep.o ./src/tool_strdup.o ./src/tool_urlglob.o ./src/tool_util.o ./src/tool_vms.o ./src/tool_writeenv.o ./src/tool_writeout.o ./src/tool_xattr.o
CFLAGS += -I./include/curl -v
#LDFLAGS += -L/home/kimonk/tnova/sw/petalinux/projects/curl_app_test/build/linux/rootfs/stage/usr/lib
#LDFLAGS += -L/opt/pkg/petalinux-v2014.4-final/tools/linux-i386/arm-xilinx-linux-gnueabi/arm-xilinx-linux-gnueabi/libc/usr/lib/ -L/opt/pkg/petalinux-v2014.4-final/tools/linux-i386/arm-xilinx-linux-gnueabi/arm-xilinx-linux-gnueabi/libc/lib/
LDLIBS += -lcurl
all: build install

build: $(APP)

$(APP): $(APP_OBJS)
	$(CC) $(LDFLAGS) -o $@ $(APP_OBJS) $(LDLIBS)

clean:
	-rm -f $(APP) *.elf *.gdb *.o

.PHONY: install image

install: $(APP)
	$(TARGETINST) -d $(APP) /bin/$(APP)

%.o: %.c
	$(CC) -c $(CFLAGS) -o $@ $<

help:
	@echo ""
	@echo "Quick reference for various supported build targets for $(INSTANCE)."
	@echo "----------------------------------------------------"
	@echo "  clean                  clean out build objects"
	@echo "  all                    build $(INSTANCE) and install to rootfs host copy"
	@echo "  build                  build subsystem"
	@echo "  install                install built objects to rootfs host copy"
