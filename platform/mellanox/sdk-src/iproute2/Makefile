.ONESHELL:
SHELL = /bin/bash

MAIN_TARGET = iproute2_1.mlnx.$(MLNX_SDK_DEB_VERSION)_$(CONFIGURED_ARCH).deb
DERIVED_TARGETS = iproute2-dev_1.mlnx.$(MLNX_SDK_DEB_VERSION)_$(CONFIGURED_ARCH).deb iproute2-dbgsym_1.mlnx.$(MLNX_SDK_DEB_VERSION)_$(CONFIGURED_ARCH).deb
PACKAGE_NAME = iproute2-3.19.0

$(addprefix $(DEST)/, $(MAIN_TARGET)): $(DEST)/% :
	# get sources
	rm -rf $(PACKAGE_NAME)-$(MLNX_SDK_VERSION)-$(MLNX_SDK_ISSU_VERSION)

	wget -c $(MLNX_SDK_SOURCE_BASE_URL)/$(PACKAGE_NAME)-$(MLNX_SDK_VERSION)-$(MLNX_SDK_ISSU_VERSION).tar.gz -O - | tar -xz

	# build
	pushd $(PACKAGE_NAME)-$(MLNX_SDK_VERSION)-$(MLNX_SDK_ISSU_VERSION)

	if [ -f autogen.sh ]; then
		./autogen.sh
	fi

	debuild -b -us -uc -j$(SONIC_CONFIG_MAKE_JOBS)

	popd

	mv $(DERIVED_TARGETS) $* $(DEST)/

$(addprefix $(DEST)/, $(DERIVED_TARGETS)): $(DEST)/% : $(DEST)/$(MAIN_TARGET)
