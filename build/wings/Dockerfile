FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8
ENV GOBIN=/usr/local/go/bin

USER root
RUN apt -y update
RUN apt -y --no-install-recommends install software-properties-common gnupg2 curl sudo
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt -y update
RUN apt -y --no-install-recommends install \
        git \
        iputils-ping \
        tar \
        zip \
        nano \
        unzip \
        make \
        gcc \
        g++ \
        gdb \
        python \
        docker-ce \
        docker-ce-cli \
        containerd.io \
        iproute2 \
        net-tools
RUN curl -OL "https://go.dev/dl/go1.19.11.linux-$(dpkg --print-architecture).tar.gz" \
RUN tar xvf "go1.19.11.linux-$(dpkg --print-architecture).tar.gz" -C /usr/local \
RUN chown -R root:root /usr/local/go \
RUN rm -rf go*.gz
RUN /usr/local/go/bin/go install github.com/go-delve/delve/cmd/dlv@latest
RUN usermod -aG docker root
RUN echo "export PATH=\$PATH:/usr/local/go/bin" >> /etc/bash.bashrc

EXPOSE 8080
EXPOSE 2022

WORKDIR /home/root/wings
