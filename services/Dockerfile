FROM fedora:22

RUN dnf -y groupinstall "Development Tools" \
 && dnf -y install flex bison pkgconfig openssl-devel \
 && adduser --system --home /home/atheme atheme \
 && mkdir -p /home/atheme/src \
 && chown -R atheme /home/atheme

USER atheme

ENV ATHEME_GIT_COMMITLIKE c961688c910803158202b27d4b9237acb100f251

RUN cd /home/atheme/src \
 && git clone https://github.com/atheme/atheme \
 && cd atheme \
 && git checkout $ATHEME_GIT_COMMITLIKE \
 && git submodule update --init \
 && ./configure \
 && make \
 && make install || true

ADD atheme.conf /home/atheme/atheme/etc/

CMD /home/atheme/atheme/bin/atheme-services -n

# vim: set ts=2 sw=2 tw=0 noet :
