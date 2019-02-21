FROM debian:stable
WORKDIR /scratch
RUN apt-get update
RUN apt-get -y install wget lbzip2
RUN wget -r -l1 --no-parent -nd -A'stage3-amd64-musl-vanilla-*.tar.bz2' http://distfiles.gentoo.org/experimental/amd64/musl/
RUN wget http://distfiles.gentoo.org/snapshots/portage-latest.tar.bz2
RUN tar xf stage3-amd64-musl-vanilla-*.tar.bz2
RUN tar xf portage-latest.tar.bz2 -Cusr
RUN rm stage3-amd64-musl-vanilla-*.tar.bz2 portage-latest.tar.bz2

FROM scratch
COPY --from=0 /scratch /
CMD /bin/bash --login -i
RUN echo 'MAKEOPTS="-j20"' >> /etc/portage/make.conf                                            && \
    cat /etc/portage/make.conf                                                                  && \
    emerge --sync
