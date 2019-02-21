FROM mhier/docker-non-gnu-gentoo:clang-installed
RUN echo 'CC="clang"' >> /etc/portage/make.conf                                                 && \
    echo 'CXX="clang++"' >> /etc/portage/make.conf                                              && \
    echo 'AR="llvm-ar"' >> /etc/portage/make.conf                                               && \
    echo 'NM="llvm-nm"' >> /etc/portage/make.conf                                               && \
    echo 'RANLIB="llvm-ranlib"' >> /etc/portage/make.conf                                       && \
    emerge -ev @world
