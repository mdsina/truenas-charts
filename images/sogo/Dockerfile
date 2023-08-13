FROM dokken/centos-stream-9:latest

COPY sogo.pgp /etc/sogo/
RUN rpm --import "/etc/sogo/sogo.pgp"
RUN rpm --import "https://keys.openpgp.org/vks/v1/by-fingerprint/74FFC6D72B925A34B5D356BDF8A27B36A6E2EAE9"
COPY SOGo.repo /etc/yum.repos.d/

RUN cat /etc/yum.repos.d/SOGo.repo

RUN dnf install -y epel-release && dnf update -y
RUN dnf install -y yum-utils && dnf config-manager --set-enabled crb
RUN sed -i '/enabled=1/a exclude=gnustep* ytnef*' /etc/yum.repos.d/epel.repo

RUN dnf install sogo -y && dnf remove yum-utils epel-release -y && dnf clean all


EXPOSE 80 443 20000
ENV JWT=;
ENV WORKERS=3

COPY run-sogo /usr/local/bin/

CMD ["run-sogo"]
