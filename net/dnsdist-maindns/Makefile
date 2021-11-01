#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dnsdist-maindns
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

PKG_MAINTAINER:=Peter van Dijk <peter.van.dijk@powerdns.com>

define Package/dnsdist-maindns
	SECTION:=net
	CATEGORY:=Network
	TITLE:=This package disables dnsmasq so dnsdist can become the main DNS on the CPE
	URL:=http://dnsdist.org
	DEPENDS:=dnsdist odhcpd
	PKGARCH:=all
endef

define Package/dnsdist-maindns/description
	This package disables dnsmasq so dnsdist can become the main DNS on the CPE
endef

define Build/Compile
	echo nothing to do here
endef

define Package/dnsdist-maindns/install
# 	$(INSTALL_DIR) $(1)/etc
# 	touch $(1)/etc/dnsdist-maindns-installed
endef

define Package/dnsdist-maindns/postinst
#!/bin/sh

uci set 'dhcp.@dnsmasq[0].port=5353'
uci set 'dhcp.@dnsmasq[0].disabled=1'
uci set dhcp.odhcpd.maindhcp=1
uci set dhcp.lan.dhcpv4=server
uci commit dhcp
uci set dnsdist.general.enabled=1
uci commit dnsdist
/etc/init.d/dnsmasq disable
/etc/init.d/dnsdist enable || true

echo
echo dnsmasq disabled, odhcpd set up, dnsdist enabled
echo Please reboot
echo

endef

$(eval $(call BuildPackage,dnsdist-maindns))
