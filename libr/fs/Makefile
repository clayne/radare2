NAME=r_fs
R2DEPS=r_util r_io r_socket r_hash r_cons r_crypto
CFLAGS:=-DR2_PLUGIN_INCORE -Iarch/include -Iarch $(CFLAGS)

SHLR=../../shlr/

include ../config.mk
CFLAGS:=-I$(SHLR)/grub/include $(CFLAGS)
ifeq ($(WITH_GPL),1)
LDFLAGS+=$(SHLR)/grub/libgrubfs.a
endif

EXTRA_TARGETS=plugins
foo:
	for TARGET in pre plugins ${LIBSO} ${LIBAR} ; do ${MAKE} $$TARGET ; done

include ${STATIC_FS_PLUGINS}
STATIC_OBJS=$(subst ..,p/..,$(subst fs_,p/fs_,$(STATIC_OBJ)))
OBJS=${STATIC_OBJS} fs.o fs_file.o shell.o
#p/grub/main.o

#p/grub/libgrubfs.a:
#	cd p/grub && ${MAKE} libgrubfs.a CC="${CC}"

pre:
	cd d && ${MAKE}
#	@if [ ! -e libr_fs.${EXT_SO} ]; then if [ ! -e libr_fs.${EXT_AR} ]; then rm -f ${STATIC_OBJS} ; fi ; fi

re:
	rm -f fs.o libr_fs.so
	${MAKE}
	rm -f t/fastcall.o
	sudo ${MAKE} install
	cd t && ${MAKE}

test:
	#valgrind r2 -i test.rsc /tmp/test.fs.img
	gdb --args r2 -i test.rsc /tmp/test.fs.img

plugins:
	#cd p/grub && ${MAKE} libgrubfs.a CC="${CC}"
	cd p && ${MAKE} all

include ../rules.mk
