ALLTARGETS = clean getdata ipk

include ../../Mk/pkgdata.mk

DEPS =

BUILD_CMD = /bin/false

INSTALL_CMD = /bin/false

GETDATA_TARARGS = --exclude=usr/local/include/python3.6m/pyconfig.h \
		  usr/local/include/python3.6m \
		  usr/local/lib/pkgconfig/python*3* \
		  usr/local/lib/python3.6/config-3.6m-arm-linux-gnueabi/libpython3.6m.a

include ${BUILD_ROOT}/Mk/remote_build.mk
include ${BUILD_ROOT}/Mk/ipk.mk
