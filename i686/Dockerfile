FROM alpine AS build

ARG GCC_VERSION=14.2.0
ARG BIN_VERSION=2.42

ARG PREFIX=/usr
ARG TARGET=i686-elf

WORKDIR /tmp

RUN wget    https://ftp.gnu.org/gnu/gcc/gcc-${GCC_VERSION}/gcc-${GCC_VERSION}.tar.xz \
            https://ftp.gnu.org/gnu/binutils/binutils-${BIN_VERSION}.tar.xz

RUN apk update && apk add --no-cache --update alpine-sdk xz mpfr-dev gmp-dev mpc1-dev nasm && \
    tar xf binutils-${BIN_VERSION}.tar.xz && cd binutils-${BIN_VERSION} && \
    ./configure --target=${TARGET} --prefix="${PREFIX}" --with-sysroot --disable-nls --disable-werror && \
    make -j8 && make install && cd .. && \
    tar xf gcc-${GCC_VERSION}.tar.xz && cd gcc-${GCC_VERSION}/ && mkdir build && cd build && \
    ../configure --target=${TARGET} --prefix="${PREFIX}" --disable-nls --enable-languages=c,c++ --without-headers && \
    make all-gcc all-target-libgcc -j8 && make install-gcc install-target-libgcc && \
    cd .. && cd ..


FROM alpine

COPY --from=build /usr /usr

ENTRYPOINT [ "sh" ]