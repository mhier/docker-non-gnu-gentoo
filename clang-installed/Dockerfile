FROM gentoo-clang/base
RUN echo 'USE="clang libcxx default-libcxx -sanitize"' >> /etc/portage/make.conf                && \
    cat /etc/portage/make.conf                                                                  && \
    emerge --update --deep --changed-use sys-devel/clang
