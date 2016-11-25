ifndef PETALINUX
$(error "Error: PETALINUX environment variable not set.  Change to the root of your PetaLinux install, and source the settings.sh file")
endif

include libs.common.mk

LIB=libcurl

# Add any other object files to this list below
# LIB_OBJS = libcurl.o
#LIB_OBJS = ./lib/amigaos.o ./lib/escape.o ./lib/file.o ./lib/asyn-ares.o ./lib/asyn-thread.o ./lib/base64.o ./lib/conncache.o ./lib/connect.o ./lib/content_encoding.o ./lib/cookie.o ./lib/curl_addrinfo.o ./lib/curl_des.o ./lib/curl_endian.o ./lib/curl_fnmatch.o ./lib/curl_gethostname.o ./lib/curl_gssapi.o

LIB_OBJS = ./lib/smtp.o ./lib/amigaos.o ./lib/escape.o ./lib/file.o ./lib/asyn-ares.o ./lib/asyn-thread.o ./lib/base64.o ./lib/conncache.o ./lib/connect.o ./lib/content_encoding.o ./lib/cookie.o ./lib/curl_addrinfo.o ./lib/curl_des.o ./lib/curl_endian.o ./lib/curl_fnmatch.o ./lib/curl_gethostname.o ./lib/curl_gssapi.o ./lib/curl_memrchr.o ./lib/curl_multibyte.o ./lib/curl_ntlm.o ./lib/curl_ntlm_core.o ./lib/curl_ntlm_msgs.o ./lib/curl_ntlm_wb.o ./lib/curl_rtmp.o ./lib/curl_sasl.o ./lib/curl_sasl_gssapi.o ./lib/curl_sspi.o ./lib/curl_threads.o ./lib/dict.o ./lib/dotdot.o ./lib/easy.o ./lib/fileinfo.o ./lib/formdata.o ./lib/ftp.o ./lib/ftplistparser.o ./lib/getenv.o ./lib/getinfo.o ./lib/gopher.o ./lib/hash.o ./lib/hmac.o ./lib/hostcheck.o ./lib/hostip.o ./lib/hostip4.o ./lib/hostip6.o ./lib/hostsyn.o ./lib/http.o ./lib/http2.o ./lib/http_chunks.o ./lib/http_digest.o ./lib/http_negotiate.o ./lib/http_negotiate_sspi.o ./lib/http_proxy.o ./lib/idn_win32.o ./lib/if2ip.o ./lib/imap.o ./lib/inet_ntop.o ./lib/inet_pton.o ./lib/krb5.o ./lib/ldap.o ./lib/llist.o ./lib/md4.o ./lib/md5.o ./lib/memdebug.o ./lib/mprintf.o ./lib/multi.o ./lib/netrc.o ./lib/non-ascii.o ./lib/nonblock.o ./lib/nwlib.o ./lib/nwos.o ./lib/openldap.o ./lib/parsedate.o ./lib/pingpong.o ./lib/pipeline.o ./lib/pop3.o ./lib/progress.o ./lib/rawstr.o ./lib/rtsp.o ./lib/security.o ./lib/select.o ./lib/sendf.o ./lib/share.o ./lib/slist.o ./lib/smb.o ./lib/socks.o ./lib/socks_gssapi.o ./lib/socks_sspi.o ./lib/speedcheck.o ./lib/splay.o ./lib/ssh.o ./lib/strdup.o ./lib/strequal.o ./lib/strerror.o ./lib/strtok.o ./lib/strtoofft.o ./lib/telnet.o ./lib/tftp.o ./lib/timeval.o ./lib/url.o ./lib/version.o ./lib/warnless.o ./lib/wildcard.o ./lib/x509asn1.o ./lib/transfer.o ./lib/vtls/axtls.o ./lib/vtls/cyassl.o ./lib/vtls/darwinssl.o ./lib/vtls/gskit.o ./lib/vtls/mbedtls.o ./lib/vtls/nss.o ./lib/vtls/openssl.o ./lib/vtls/polarssl.o ./lib/vtls/polarssl_threadlock.o ./lib/vtls/schannel.o ./lib/vtls/vtls.o
 
LIB_HEADERS := \
	./include/curl/curlbuild.h \
	./include/curl/curl.h \
	./include/curl/curlrules.h \
	./include/curl/curlver.h \
	./include/curl/easy.h \
	./include/curl/mprintf.h \
	./include/curl/multi.h \
	./include/curl/stdcheaders.h \
	./include/curl/typecheck-gcc.h

CFLAGS := -I./include -fPIC -v

all: build install

.PHONY: build
build: $(LIB).a $(LIB).so
	# Install libraries
	mkdir -p $(STAGEDIR)/usr/lib
	rsync -a *.a $(STAGEDIR)/usr/lib/
	rsync -a *.so $(STAGEDIR)/usr/lib/
	rsync -a  *.so.* $(STAGEDIR)/usr/lib/
	
	# Install headers
	mkdir -p $(STAGEDIR)/usr/include
	for h in $(LIB_HEADERS); do \
		rsync -a $$h $(STAGEDIR)/usr/include; \
	done

$(LIB).a:$(LIB_OBJS)
	$(AR) rcs $@ $(LIB_OBJS)

$(LIB).so:$(LIB_OBJS)
	$(CC) -shared -o $@.1.0.1 $(LIB_OBJS)
	rm -f $@.1 $@
	ln -s $@.1.0.1 $@.1
	ln -s $@.1.0.1 $@

%.o: %.c
	$(CC) -c $(CFLAGS) -o $@ $<
	
install: $(LIB).so
	# Install libraries template
	# Install lib files
	$(TARGETINST) -d $<.1.0.1 /lib/$<.1.0.1
	# Install lib symlink
	$(TARGETINST) -s $<.1.0.1 /lib/$<.1
	$(TARGETINST) -s $<.1.0.1 /lib/$<

clean:
	rm -rf *.o *.so *.so.* *.a

help:
	@echo ""
	@echo "Quick reference for various supported build targets for $(INSTANCE)."
	@echo "----------------------------------------------------"
	@echo "  clean                  clean out build objects"
	@echo "  all                    build $(INSTANCE) and install to rootfs host copy"
	@echo "  build                  build subsystem"
	@echo "  install                install built objects to rootfs host copy"
