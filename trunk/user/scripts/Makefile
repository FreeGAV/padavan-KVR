THISDIR = $(shell pwd)
all:

clean:

romfs:
	./makedevlinks $(ROMFSDIR)
	$(ROMFSINST) /sbin/radio2_kicksta
	$(ROMFSINST) /sbin/dev_init.sh
	$(ROMFSINST) /sbin/reset_ss.sh
	$(ROMFSINST) -p +x $(THISDIR)/wgetcurl.sh /sbin/wgetcurl.sh
	$(ROMFSINST) /sbin/mtd_storage.sh
	$(ROMFSINST) -p +x $(THISDIR)/check_disk_size /sbin/check_disk_size
	$(ROMFSINST) -p +x $(THISDIR)/copyscripts.sh /usr/bin/copyscripts.sh
	$(ROMFSINST) -p +x $(THISDIR)/autostart.sh /usr/bin/autostart.sh
	$(ROMFSINST) -p +x $(THISDIR)/ap_script.sh /etc_ro/ap_script.sh
	$(ROMFSINST) -p +x $(THISDIR)/sh_ezscript.sh /etc_ro/sh_ezscript.sh
	$(ROMFSINST) -p +x $(THISDIR)/sysinfo.sh /etc_ro/sysinfo.sh
ifeq ($(STORAGE_ENABLED),y)
	$(ROMFSINST) /sbin/automount.sh
endif
ifdef CONFIG_BLK_DEV_SD
	$(ROMFSINST) /sbin/hddtune.sh
	$(ROMFSINST) /sbin/spindown.sh
endif
ifdef CONFIG_MTD_UBI
	$(ROMFSINST) /sbin/rwfs2ubi.sh
endif
	$(ROMFSINST) /etc_ro/protocols
	$(ROMFSINST) /etc_ro/services
	$(ROMFSINST) /etc_ro/profile
	$(ROMFSINST) /etc_ro/shells
	$(ROMFSINST) /etc_ro/mdev.conf
	$(ROMFSINST) /etc_ro/banner
	mkdir -p $(INSTALLDIR)/usr/share/terminfo
	tar -xzf ./terminfo.tar.gz -C $(INSTALLDIR)/usr/share
	$(ROMFSINST) /sbin/check_crontab.sh
	$(ROMFSINST) $(THISDIR)/certs.tgz /etc_ro/certs.tgz
