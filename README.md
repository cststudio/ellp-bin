binary output for ellp -- ellp配套二进制文件
=============

## 内容
* 交叉编译器 6.3.0  
  * arm-unknown-linux-gnueabihf.tar.bz2.[0|1]：压缩包，因大小限制，分为两个文件。  
* imx6ul&imx6q 内核
* vexpress a9 内核

## imx6
```
imx6q:  
qemu-system-arm -M sabrelite -nographic -m 512M \
-kernel ./zImage \
-dtb ./dts/imx6q-sabrelite.dtb \
-append "earlyprintk=vga log_buf_len=25M console=ttymxc0,115200 rootfstype=ext3 root=/dev/mmcblk1 rw rootwait init=/sbin/init" \
-drive file=rootfs.img,format=raw,id=mycard -device sd-card,drive=mycard \
-net nic,macaddr=6c:61:74:65:6c:65 -net tap,ifname=tap0

imx6ul:  
qemu-system-arm -M mcimx6ul-evk -nographic -m 512M \
-kernel ./zImage \
-dtb ./dts/imx6ul-14x14-evk.dtb \
-append "earlyprintk=vga log_buf_len=25M console=ttymxc0,115200 rootfstype=ext3 root=/dev/mmcblk1 rw rootwait init=/sbin/init" \
-drive file=rootfs.img,format=raw,id=mycard -device sd-card,drive=mycard \
-net nic,macaddr=6c:61:74:65:6c:65 -net tap,ifname=tap0
```

## 交叉编译器
arm交叉编译器二进制压缩包，由croostool-ng制作得到。  

### 使用
1、下载本工程到任意目录，此处假定为$HOME/x-tool，进入该目录，再解压： 
```
cd ~/x-tools
cat arm-unknown-linux-gnueabihf.tar.bz2.* | tar xj
```

2、将`export PATH=$HOME/x-tools/arm-unknown-linux-gnueabihf/bin:$PATH`写到`~/.bashrc`文件末尾。

3、执行`source ~/.bashrc`或重启机器让交叉编译器生效。  


### 版本
```
$ arm-linux-gcc -v
Using built-in specs.
COLLECT_GCC=arm-linux-gcc
COLLECT_LTO_WRAPPER=/home/latelee/x-tools/arm-unknown-linux-gnueabihf/libexec/gcc/arm-unknown-linux-gnueabihf/6.3.0/lto-wrapper
Target: arm-unknown-linux-gnueabihf
Configured with: /opt/ellp/crosstool-ng/.build/src/gcc-6.3.0/configure --build=x86_64-build_pc-linux-gnu --host=x86_64-build_pc-linux-gnu --target=arm-unknown-linux-gnueabihf --prefix=/home/latelee/x-tools/arm-unknown-linux-gnueabihf --with-sysroot=/home/latelee/x-tools/arm-unknown-linux-gnueabihf/arm-unknown-linux-gnueabihf/sysroot --enable-languages=c,c++ --with-fpu=neon --with-float=hard --with-pkgversion='crosstool-NG crosstool-ng-1.23.0' --disable-sjlj-exceptions --enable-__cxa_atexit --disable-libmudflap --disable-libgomp --disable-libssp --disable-libquadmath --disable-libquadmath-support --disable-libsanitizer --disable-libmpx --with-gmp=/opt/ellp/crosstool-ng/.build/arm-unknown-linux-gnueabihf/buildtools --with-mpfr=/opt/ellp/crosstool-ng/.build/arm-unknown-linux-gnueabihf/buildtools --with-mpc=/opt/ellp/crosstool-ng/.build/arm-unknown-linux-gnueabihf/buildtools --with-isl=/opt/ellp/crosstool-ng/.build/arm-unknown-linux-gnueabihf/buildtools --enable-lto --with-host-libstdcxx='-static-libgcc -Wl,-Bstatic,-lstdc++,-Bdynamic -lm' --enable-threads=posix --enable-target-optspace --enable-plugin --enable-gold --disable-nls --disable-multilib --with-local-prefix=/home/latelee/x-tools/arm-unknown-linux-gnueabihf/arm-unknown-linux-gnueabihf/sysroot --enable-long-long
Thread model: posix
gcc version 6.3.0 (crosstool-NG crosstool-ng-1.23.0) 
```