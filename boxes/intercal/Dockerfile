FROM esolang/build-base

ENV BUILD_PACKAGES="autoconf automake m4 libtool texinfo" \
    RUNTIME_PACKAGES="" \
    VERSION="0.31"

RUN apk add $BUILD_PACKAGES $RUNTIME_PACKAGES && \
    cd /tmp && \
    curl -m $TIMEOUT https://gitlab.com/esr/intercal/-/archive/${VERSION}/intercal-${VERSION}.tar.gz -LO && \
    mkdir -p ~/intercal && \
    tar xzf intercal-${VERSION}.tar.gz -C ~/intercal && \
    mv ~/intercal/intercal-${VERSION}/ ~/intercal/intercal-latest/ && \
    cd ~/intercal/intercal-latest && \
# See also: https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=intercal
# See also: https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=c-intercal
# See also: https://gitweb.gentoo.org/repo/gentoo.git/tree/dev-lang/c-intercal/files
    sed -i -e 's/0.30/0.31/' configure.ac && \
    sed -i -e 's/int yydebug/extern &/' src/perpet.c && \
    cd buildaux && ./regenerate-build-system.sh && cd .. && \
# gcc 10 fliped the default option about global variable
# https://wiki.gentoo.org/wiki/Gcc_10_porting_notes/fno_common
# BTS: https://gitlab.com/esr/intercal/-/issues/4
    CFLAGS=-fcommon ./configure && \
    make && make install && \
    apk del $BUILD_PACKAGES && \
    rm -rf /var/cache/apk/* /tmp/* && \
    ln -s /bin/script /bin/intercal

COPY script /root/script
