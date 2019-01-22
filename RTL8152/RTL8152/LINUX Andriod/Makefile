#
#
#

ifneq ($(KERNELRELEASE),)
	obj-m	 := r8152.o
else
	KERNELDIR ?= /lib/modules/$(shell uname -r)/build
	PWD :=$(shell pwd)

.PHONY: modules
modules:
	$(MAKE) -C $(KERNELDIR) SUBDIRS=$(PWD) modules

.PHONY: all
all: clean modules install

.PHONY: clean
clean:
	$(MAKE) -C $(KERNELDIR) SUBDIRS=$(PWD) clean

.PHONY: install
install:
ifneq ($(shell lsmod | grep r8152),)
	rmmod r8152
endif
	$(MAKE) -C $(KERNELDIR) SUBDIRS=$(PWD) INSTALL_MOD_DIR=kernel/drivers/net/usb modules_install
	modprobe r8152

.PHONY: install_rules
install_rules:
	install --group=root --owner=root --mode=0644 50-usb-realtek-net.rules /etc/udev/rules.d/

endif

