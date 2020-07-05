FROM i386/ubuntu:16.04
COPY ./sources.list /etc/apt/sources.list
COPY ./qemu /usr/local/bin/qemu/
WORKDIR /usr/local/bin/qemu/
RUN apt-get update \
   && apt-get install -y build-essential gdb \
# 官方指示gcc版本是 4.6.2；64位系统需要替换 gcc 为 gcc-multilib
   git \
   libsdl1.2-dev libtool-bin libglib2.0-dev libz-dev libpixman-1-dev \
   libfdt-dev \
   && gcc -m32 -print-libgcc-file-name \
   && mkdir /6.828 \
   && mkdir /usr/gnemul/ \
# 32 位系统不能模拟64位
# && ./configure --disable-kvm --disable-werror --prefix=/usr/gnemul/ --target-list="i386-softmmu x86_64-softmmu" \
   && ./configure --disable-kvm --disable-werror --prefix=/usr/gnemul/ --target-list="i386-softmmu" \
   && make \
   && make install \
   && ln -s /usr/gnemul/bin/qemu-system-i386 /usr/bin/qemu
WORKDIR /6.828
