# GL-MT6000 custom OpenWrt firmware builder

This repository automates the process of building OpenWrt custom firmware images for **MY** Flint 2 (GL-MT6000) router, based on **MY PREFERENCES** and [pesa1234](https://github.com/pesa1234)'s work.

You should **not use** the firmwares released in this repository unless you have the same preferences/needs.
Instead, **make a fork and adapt to your needs**.

Read [this topic](https://forum.openwrt.org/t/mt6000-custom-build-with-luci-and-some-optimization-kernel-6-12-x/185241) in OpenWrt's forum to learn the details about pesa1234's customizations.

Compared to his custom firmware, this firmware adds:
- **WiFi UCODE scripts** (faster boot)
- **Wireguard VPN**
- **Policy Based Routing** (select what goes through VPN and what not)
- **AdBlock Fast** (ads and malware blocking at DNS level)

And also:
- **REMOVED:** odhcp, upnp, iptables, avahi, samba, usb storage, and probably more stuff I forgot to mention.
- IPv6 disabled and partially removed (only because it's not possible to remove IPv6 support completely).
- Some compiler optimizations and build hardening options (cortex-a53 + crc + crypto; LTO, MOLD, and more).
- SSH configuration with strong algorithms and key exchange methods, **also IPv6 disabled**. Check the content of [`ssh_hardening.config`](files/etc/ssh/sshd_config.d/ssh_hardening.conf) and [`sshd_config`](files/etc/sshd_config).
- Quality-of-life enhancements through UCI configuration. Check the content of [`999-QOL_config`](files/etc/uci-defaults/999-QOL_config).
- Some debug and kernel stuff removed.

Check the content of [`mt6000.config`](mt6000.config) and [`sysctl.conf`](files/etc/sysctl.conf).


## Motivation

I use NordVPN in my router, together with AdBlock Fast, to protect all my devices at home.
Unfortunately, NordVPN does not support IPv6 (yet), so it is better to have it disabled to avoid IP/DNS leaks. Besides that, I noticed that if I leave IPv6 enabled my PC will randomly lose connectivity for a few seconds, frequently enough to be annoying.

I also enjoy optimizing the firmware, so I avoid packages that I don't use. Less packages also mean smaller firmware size, faster boot, more free RAM and less "open doors" for attacks. Or not so much, but it's a fun challenge.


## About SSH Hardening

To enhance the security of SSH connections, this firmware includes a hardened SSH configuration. The configuration is derived from recommendations by [SSH-Audit](https://github.com/jtesta/ssh-audit) and the [BSI](https://www.bsi.bund.de/), it specifies strong key exchange algorithms, ciphers, message authentication codes (MACs), host key algorithms, and public key algorithms. This ensures that only secure and up-to-date algorithms are used for SSH communication.


## Contributing

Contributions to this project are welcome. If you encounter any issues or have suggestions for improvements, please open an issue or submit a pull request on the GitHub repository.


## Acknowledgements

- The OpenWrt project for providing the foundation for this firmware build and support of [GL.iNet GL-MT6000](https://openwrt.org/toh/gl.inet/gl-mt6000) router.
- The community over at the [OpenWrt forum](https://forum.openwrt.org/t/mt6000-custom-build-with-luci-and-some-optimization-kernel-6-12-x/185241) for their valuable contributions and resources. 
- [pesa1234](https://github.com/pesa1234) for his [MT6000 custom builds](https://github.com/pesa1234/MT6000_cust_build).
- [Julius Bairaktaris](https://github.com/JuliusBairaktaris/Qualcommax_NSS_Builder) from whom I "borrowed" much of this project (his repository is about custom builds for Xiaomi AX3600).
