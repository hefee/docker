FROM fedora:21

#System deps
RUN yum -y install sudo yum-utils
RUN yum -y install gcc-c++ git doxygen cmake bzr vim tar
RUN yum -y install qt4-devel automoc phonon-devel qtwebkit-devel attica-devel dbusmenu-qt-devel strigi-devel qjson-devel libcurl-devel xsd xerces xapian-core-devel kdelibs-devel
#kdesrcbuild deps
RUN yum -y install sudo perl-libwww-perl perl-JSON perl-XML-Parser
#up until kdelibs
RUN yum-builddep -y kdelibs
#PIM deps
RUN yum -y install boost-devel sqlite prison-devel openldap-devel libical-devel libical-devel gpgme-devel

RUN useradd -d /home/developer -m developer
RUN mkdir /work /qt
RUN chown developer /work /qt

# some symlinks in /root to handle sudo ./kdesrc-build
RUN ln -s /home/developer/.kdesrc-buildrc /root/.kdesrc-buildrc && \
    ln -s /home/developer/kdesrc-build /root/kdesrc-build
# setup developer account
RUN echo 'developer ALL=NOPASSWD: ALL' >> /etc/sudoers
USER developer
ENV HOME /home/developer
WORKDIR /home/developer/
# kde anongit url alias
RUN git config --global url."git://anongit.kde.org/".insteadOf kde: && \
    git config --global url."ssh://git@git.kde.org/".pushInsteadOf kde: && \
    git clone git://anongit.kde.org/kdesrc-build.git

VOLUME /work
VOLUME /qt

ENTRYPOINT ["/bin/bash"]
