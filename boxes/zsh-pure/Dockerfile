FROM esolang/build-base

ENV BUILD_PACKAGES="zsh libcap2" \
    RUNTIME_PACKAGES="python3"

RUN apk add $BUILD_PACKAGES $RUNTIME_PACKAGES && \
    wget https://olivier.sessink.nl/jailkit/jailkit-2.23.tar.gz && \
    tar xf jailkit-2.23.tar.gz && \
    cd jailkit-2.23 && \
    ./configure && make && make install && \
    mkdir -p /opt/jails/zsh-pure && \
    jk_init -j /opt/jails/zsh-pure uidbasics && \
    mkdir -p /opt/jails/zsh-pure/bin && \
    cp /bin/zsh /opt/jails/zsh-pure/bin/ && \
    mkdir -p /opt/jails/zsh-pure/lib && \
    cp /lib/ld-musl-x86_64.so.1 /opt/jails/zsh-pure/lib/ && \
    cp /usr/lib/libncursesw.so.6 /opt/jails/zsh-pure/lib/ && \
    cp /usr/lib/libcap.so.2 /opt/jails/zsh-pure/lib/ && \
    apk del $BUILD_PACKAGES && \
    rm -rf /var/cache/apk/* /tmp/* && \
    ln -s /bin/script /bin/zsh-pure

COPY script /root/script
