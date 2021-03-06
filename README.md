These are prebuilt WiFi modules for OpenWrt, including:
mt7603/mt7603e/mt7610/mt7610e/mt76x2e/mt7612/mt7615/mt7615e/mt7620/mt7628/mt7628sta

# How can I use them?
I assume that you already have a working OpenWrt workspace, then add the following line into "feeds.conf.default" (You will find it under the top dir of your workspace).

    src-git mtk https://github.com/luuhungit/mtk-wireless-driver.git

then execute:

	scripts/feeds update -f mtk
	scripts/feeds install -a -p mtk

Now you will be able to see extra packages via `make menuconfig`. All packages from this feeds are located under `MTK Properties`.

### uci2dat
An application that translates "/etc/config/wireless" into MTK's WiFi profiles (e.g. mt7620.dat). You may use it as an adapter to make MTK's WiFi drivers work with standard LuCi's WiFi management.

### wificonf
An application that reads/writes configuration files with "<Key>=[Value]" syntax. It can be used in your own scripts to help manipulate MTK WiFi profiles.

### mtk-nvram
The term "nvram" in MTK's software means a raw storage scheme on flash chips. It access flash device in raw mode (without filesystem). 
All data stored in nvram partition are "<Key>=[Value]" pairs. It usually resides in mtd partition "config". 
Note： OpenWrt has replaced nvram scheme with [uci](https://wiki.openwrt.org/doc/uci) long ago. I keep this for back compatibility only. 

### mtk-luci-plugin
This is a plugin for LuCI web interface, which manipulates MTK's proprietary drivers by reading/writing its profile directly. It does not use uci, so "/etc/config/wireless" is left untouched.
