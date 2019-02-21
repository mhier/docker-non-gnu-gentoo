FROM builder:bionic
WORKDIR /scratch
RUN apt-get update
RUN apt-get -y install wget
RUN wget -r -l1 --no-parent -nd -A'stage3-amd64-musl-vanilla-*.tar.bz2' http://distfiles.gentoo.org/experimental/amd64/musl/
RUN wget http://distfiles.gentoo.org/snapshots/portage-latest.tar.bz2
RUN tar xf stage3-amd64-musl-vanilla-*.tar.bz2
RUN tar xf portage-latest.tar.bz2 -Cusr
RUN rm stage3-amd64-musl-vanilla-*.tar.bz2 portage-latest.tar.bz2

FROM scratch
COPY --from=0 /scratch /
CMD /bin/bash --login --interactive
RUN echo 'http_proxy="http://xfelproxy.desy.de:3128"' >> /etc/portage/make.conf                 && \
    echo 'ftp_proxy="http://xfelproxy.desy.de:3128"' >> /etc/portage/make.conf                  && \
    echo 'MAKEOPTS="-j20"' >> /etc/portage/make.conf                                            && \
    echo 'USE="clang libcxx default-libcxx -sanitize"' >> /etc/portage/make.conf                && \
    cat /etc/portage/make.conf                                                                  && \
    emerge-webrsync                                                                             && \
    emerge --update --deep --changed-use sys-devel/clang
RUN echo 'CC="clang"'                                                                           && \
    echo 'CXX="clang++"'                                                                        && \
    echo 'CFLAGS="${CFLAGS} -flto"'                                                             && \
    echo 'CXXFLAGS="${CXXFLAGS} -flto"'                                                         && \
    echo 'LDFLAGS="-Wl,-O2 -Wl,--as-needed"'                                                    && \
    echo 'AR="llvm-ar"'                                                                         && \
    echo 'NM="llvm-nm"'                                                                         && \
    echo 'RANLIB="llvm-ranlib"'                                                                 && \
    emerge --update --deep --changed-use @world
