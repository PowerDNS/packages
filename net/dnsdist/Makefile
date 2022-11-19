include $(TOPDIR)/rules.mk

PKG_NAME:=dnsdist
PKG_VERSION:=1.8.0-alpha0.1940.master.g8dedccd5d
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://downloads.powerdns.com/autobuilt/dnsdist/1.8.0-alpha0.1940.master.g8dedccd5d/
PKG_HASH:=22932115c7f061f92ab4e70e680df71b43ba355a3b342057c11d4c7bda76c2f2

PKG_MAINTAINER:=Peter van Dijk <peter.van.dijk@powerdns.com>
PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:powerdns:dnsdist

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=boost

PKG_CONFIG_DEPENDS:= \
  CONFIG_DNSDIST_GNUTLS \
  CONFIG_DNSDIST_OPENSSL

include $(INCLUDE_DIR)/package.mk

define Package/dnsdist/config
menu "Configuration"
	depends on PACKAGE_dnsdist

	comment "SSL Support"
	choice
		prompt "Selected SSL library"
		default DNSDIST_OPENSSL

		config DNSDIST_OPENSSL
			bool "OpenSSL"

		config DNSDIST_GNUTLS
			bool "GnuTLS"

		config DNSDIST_NOSSL
			bool "No SSL support"

	endchoice

	comment "DNS over HTTPS/TLS Support"
	depends on !DNSDIST_NOSSL

	config DNSDIST_DNS_OVER_HTTPS
	depends on DNSDIST_OPENSSL
	depends on !DNSDIST_NOSSL
		bool "DNS over HTTPS Support"
		help
			"Enables DNS over HTTPS Support for dnsdist"
		default y

	config DNSDIST_DNS_OVER_HTTPS_OUTGOING
	depends on DNSDIST_OPENSSL
	depends on !DNSDIST_NOSSL
		bool "Outgoing DNS over HTTPS Support"
		help
			"Enables Outgoing DNS over HTTPS Support for dnsdist"
		default y

	config DNSDIST_DNS_OVER_TLS
	depends on !DNSDIST_NOSSL
		bool "DNS over TLS Support"
		help
			"Enabled DNS over TLS Support for dnsdist"
		default y

	config DNSDIST_CARBON
		bool "CARBON support"
		help
			"Enable Carbon (Graphite) support for dnsdist"
		default n

	config DNSDIST_CDB
		bool "CDB support"
		help
			"Enable CDB support for dnsdist"
		default n

	config DNSDIST_COMPLETION
		bool "Console completion support"
		help
			"Enable console completion for dnsdist"
		default n

	config DNSDIST_DEBUG_SYMBOLS
		bool "Debug symbols"
		help
			"Enable debug symbols in the dnsdist binary"
		default n

	config DNSDIST_DELAY_PIPE
		bool "Delay action support"
		help
			"Enable delay action support for dnsdist"
		default n

	config DNSDIST_DYNBLOCKS
		bool "Dynamic blocks support"
		help
			"Enable dynamic blocks support for dnsdist"
		default n

	config DNSDIST_DNSTAP
		bool "DNSTAP support"
		help
			"Enable DNSTAP support for dnsdist"
		default n

	config DNSDIST_EBPF
		bool "eBPF support"
		help
			"Enable eBPF support for dnsdist"
		default n

	config DNSDIST_ECS_ACTIONS
		bool "ECS actions"
		help
			"Enable actions that control EDNS Client Subnet support for dnsdist"
		default n

	config DNSDIST_HASHED
		bool "Hashed credentials"
		help
			"Enable credentials hashing support for dnsdist"
		default n

	config DNSDIST_IPCIPHER
		bool "IP cipher support"
		help
			"Enable IP cipher support for dnsdist"
		default n

	config DNSDIST_LIBEDIT
		bool "Build with libedit"
		help
			"Build with libedit - for completion, history and line editing"
		default n

	config DNSDIST_LMDB
		bool "LMDB support"
		help
			"Enable LMDB support for dnsdist"
		default n

	config DNSDIST_LUA_ADVANCED
		bool "Lua advanced bindings"
		help
			"Enable Lua bindings for queries and responses manipulation in dnsdist"
		default n

	config DNSDIST_MAC
		bool "MAC address support"
		help
			"Enable MAC address in ring buffers support for dnsdist"
		default y

	config DNSDIST_NET_SNMP
		bool "Net-SNMP support"
		help
			"Enable Net-SNMP support for dnsdist"
		default n

	config DNSDIST_OCSP_STAPLING
		bool "OCSP Stapling support"
		help
			"Enable OCSP Stapling support for dnsdist"
		default n

	config DNSDIST_PIE
		bool "Position Independent Executable"
		help
			"Build dnsdist as a Position-Independent executable. This is required to benefit from ASLR, but significantly increases the required disk space and memory usage"
		default y

	config DNSDIST_PROTOBUF
		bool "Protobuf support"
		help
			"Enable exporting queries and responses over Protocol Buffer for dnsdist"
		default n

	config DNSDIST_PROMETHEUS
		bool "Prometheus support"
		help
			"Enable Prometheus support for dnsdist"
		default n

	config DNSDIST_RE2
		bool "RE2 support"
		help
			"Enable RE2 support for dnsdist"
		default n

	config DNSDIST_RULES_ALTER
		bool "Rules altering queries"
		help
			"Enable rules altering queries for dnsdist"
		default n

	config DNSDIST_SECPOLL
		bool "Security polling"
		help
			"Enable security polling support for dnsdist"
		default n

	config DNSDIST_SODIUM
		bool "Build with libsodium"
		help
			"Build with libsodium - for encrypted console connections, and DNSCrypt"
		default n

	config DNSDIST_TOP_N
		bool "Top N bindings"
		help
			"Enable bindings to get the top N queries and responses in dnsdist"
		default n

	config DNSDIST_WEB
		bool "Internal web server"
		help
			"Enable support for the internal web server in dnsdist"
		default n

endmenu
endef

define Package/dnsdist
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=dnsdist DNS-, DOS- and abuse-aware loadbalancer
  USERID:=dnsdist:dnsdist
  DEPENDS:= \
	  +ca-bundle \
	  +libatomic \
	  +libcap \
	  +libstdcpp \
	  +libubox-lua \
	  +libubus-lua \
	  +libuci-lua \
	  +luajit \
	  +luafilesystem \
	  +DNSDIST_LIBEDIT:libedit \
	  +DNSDIST_DNSTAP:libfstrm \
	  +DNSDIST_GNUTLS:libgnutls \
	  +DNSDIST_DNS_OVER_HTTPS:libh2o-evloop-tiny \
	  +DNSDIST_NET_SNMP:libnetsnmp \
	  +DNSDIST_DNS_OVER_HTTPS_OUTGOING:libnghttp2 \
	  +DNSDIST_OPENSSL:libopenssl \
	  +DNSDIST_SODIUM:libsodium \
	  +DNSDIST_LMDB:lmdb \
	  +DNSDIST_CDB:tinycdb \
	  +DNSDIST_RE2:re2
  URL:=https://dnsdist.org/
endef

define Package/dnsdist/description
  dnsdist is a highly DNS-, DoS- and abuse-aware loadbalancer. Its goal in life
  is to route traffic to the best server, delivering top performance to legitimate
  users while shunting or blocking abusive traffic.
endef

define Package/dnsdist/conffiles
/etc/dnsdist.conf
/etc/config/dnsdist
/etc/init.d/dnsdist
endef

# not everything groks --disable-nls
DISABLE_NLS:=

# disable PIE for this package, see CONFIG_DNSDIST_PIE
PKG_ASLR_PIE:=0

ifneq ($(CONFIG_DNSDIST_DEBUG_SYMBOLS),)
	RSTRIP:=:
	STRIP:=:
endif

# OpenWRT's setting of CXX destroys dnsdist's -std=c++17
# --with-re2 compensates for that because it compensates for a bug in re2.pc that also destroys it
# so this addition is for the --without-re2 case
#
# none of this is pretty
TARGET_CXX+=-std=c++17
TARGET_CFLAGS+=-Os -fvisibility=hidden -flto -fno-ipa-cp -DNDEBUG
TARGET_CXXFLAGS+=-Os -fvisibility=hidden -flto -fno-ipa-cp -DNDEBUG \
	-DDISABLE_DEPRECATED_DYNBLOCK -DDISABLE_RECVMMSG -DDISABLE_NPN -DDISABLE_FALSE_SHARING_PADDING -DUSE_SINGLE_ACCEPTOR_THREAD -DOPENSSL_NO_ENGINE -DDISABLE_OPENSSL_ERROR_STRINGS \
	$(if $(CONFIG_DNSDIST_CARBON),,-DDISABLE_CARBON) \
	$(if $(CONFIG_DNSDIST_COMPLETION),,-DDISABLE_COMPLETION) \
	$(if $(CONFIG_DNSDIST_DEBUG_SYMBOLS),-g3,) \
	$(if $(CONFIG_DNSDIST_DELAY_PIPE),,-DDISABLE_DELAY_PIPE) \
	$(if $(CONFIG_DNSDIST_DYNBLOCKS),,-DDISABLE_DYNBLOCKS) \
	$(if $(CONFIG_DNSDIST_ECS_ACTIONS),,-DDISABLE_ECS_ACTIONS) \
	$(if $(CONFIG_DNSDIST_HASHED),,-DDISABLE_HASHED_CREDENTIALS) \
	$(if $(CONFIG_DNSDIST_LUA_ADVANCED),,-DDISABLE_NON_FFI_DQ_BINDINGS -DDISABLE_POLICIES_BINDINGS -DDISABLE_DOWNSTREAM_BINDINGS -DDISABLE_DNSHEADER_BINDINGS -DDISABLE_COMBO_ADDR_BINDINGS -DDISABLE_QPS_LIMITER_BINDINGS -DDISABLE_PACKETCACHE_BINDINGS -DDISABLE_CLIENT_STATE_BINDINGS -DDISABLE_DNSPACKET_BINDINGS -DDISABLE_LUA_BINDINGS_RINGS) \
	$(if $(CONFIG_DNSDIST_MAC),-DDNSDIST_RINGS_WITH_MACADDRESS,) \
	$(if $(CONFIG_DNSDIST_OCSP_STAPLING),,-DDISABLE_OCSP_STAPLING) \
	$(if $(CONFIG_DNSDIST_PROTOBUF),,-DDISABLE_PROTOBUF) \
	$(if $(CONFIG_DNSDIST_PROMETHEUS),,-DDISABLE_PROMETHEUS) \
	$(if $(CONFIG_DNSDIST_RULES_ALTER),,-DDISABLE_RULES_ALTERING_QUERIES) \
	$(if $(CONFIG_DNSDIST_SECPOLL),,-DDISABLE_SECPOLL) \
	$(if $(CONFIG_DNSDIST_TOP_N),,-DDISABLE_TOP_N_BINDINGS) \
	$(if $(CONFIG_DNSDIST_WEB),,-DDISABLE_WEB_CONFIG -DDISABLE_BUILTIN_HTML -DDISABLE_LUA_WEB_HANDLERS)

CONFIGURE_ARGS+= \
	--with-pic \
	--with-lua=luajit \
	--with-libcap \
	$(if $(CONFIG_DNSDIST_PIE),,--disable-hardening) \
	$(if $(CONFIG_DNSDIST_SODIUM),--enable-dnscrypt --with-libsodium,--disable-dnscrypt --without-libsodium) \
	$(if $(CONFIG_DNSDIST_DNSTAP),--enable-dnstap=yes,--enable-dnstap=no) \
	$(if $(CONFIG_DNSDIST_RE2),--with,--without)-re2 \
	$(if $(CONFIG_DNSDIST_NET_SNMP),--with,--without)-net-snmp \
	$(if $(CONFIG_DNSDIST_GNUTLS),--with,--without)-gnutls \
	$(if $(CONFIG_DNSDIST_OPENSSL),--with,--without)-libssl \
	$(if $(CONFIG_DNSDIST_DNS_OVER_TLS),--enable-dns-over-tls,) \
	$(if $(CONFIG_DNSDIST_CDB),--with,--without)-cdb \
	$(if $(CONFIG_DNSDIST_LMDB),--with,--without)-lmdb \
	$(if $(CONFIG_DNSDIST_LIBEDIT),--with,--without)-libedit \
	$(if $(CONFIG_DNSDIST_IPCIPHER),--enable,--disable)-ipcipher \
	$(if $(CONFIG_DNSDIST_EBPF),--with,--without)-ebpf \
	$(if $(CONFIG_DNSDIST_DNS_OVER_HTTPS),--enable-dns-over-https,) \
	$(if $(CONFIG_DNSDIST_DNS_OVER_HTTPS_OUTGOING),--with,--without)-nghttp2

define Package/dnsdist/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/dnsdist.conf.d
	$(INSTALL_CONF) ./files/dnsdist.conf $(1)/etc/dnsdist.conf
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/dnsdist.init $(1)/etc/init.d/dnsdist
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dnsdist $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/share/acl.d
	$(INSTALL_DATA) ./files/dnsdist_acl.json $(1)/usr/share/acl.d
	$(INSTALL_DIR) $(1)/usr/share/lua/dnsdist
	$(INSTALL_DIR) $(1)/usr/share/dnsdist
	$(CP) ./files/common.lua $(1)/usr/share/lua/dnsdist/
	$(CP) ./files/configuration.lua $(1)/usr/share/lua/dnsdist/
	$(CP) ./files/local-domains.lua $(1)/usr/share/lua/dnsdist/
	$(CP) ./files/os.lua $(1)/usr/share/lua/dnsdist/
	$(CP) ./files/dnsdist-odhcpd.lua $(1)/usr/share/lua/dnsdist/
	$(CP) ./files/start.lua $(1)/usr/share/lua/dnsdist/
	$(CP) ./files/sample.uci.conf $(1)/usr/share/dnsdist/sample.uci.conf
	$(CP) ./files/dnsdist.config $(1)/usr/share/dnsdist/simple.uci.conf
	$(INSTALL_BIN) ./files/diag.sh $(1)/usr/share/dnsdist/diag.sh
endef

define Package/dnsdist/postinst
#!/bin/sh
# if we are on a "real" system, IPKG_INSTROOT will be empty,
# otherwise we are in the process of building an image and
# thus on the host system
local root="$${IPKG_INSTROOT}"

if [ ! -e "$${root}/etc/config/dnsdist" ]; then
	cp "$${root}/usr/share/dnsdist/simple.uci.conf" "$${root}/etc/config/dnsdist"
fi
endef


$(eval $(call BuildPackage,dnsdist))
