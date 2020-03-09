git clone https://github.com/openwrt/openwrt.git

cd openwrt
cp -pv ~/friendlywrt-h5/configs/config_h5 ./.config

make defconfig
./scripts/feeds update -a && ./scripts/feeds install -a

make menuconfig
make -j9 target/linux/compile

find . -name "*neo-plus2.dts"
cp -pv ~/openwrt/sun50i-h5-nanopi-neo-plus2.dts.patched ./build_dir/target-aarch64_cortex-a53_musl/linux-sunxi_cortexa53/linux-4.19.106/arch/arm64/boot/dts/allwinner/sun50i-h5-nanopi-neo-plus2.dts

make -j9 download world
