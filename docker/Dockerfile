FROM ubuntu:20.04

RUN apt update 
RUN DEBIAN_FRONTEND=noninteractive apt install -y fzf git ruby python3-pip curl net-tools git unzip xsltproc wget
RUN wget -O /usr/bin/jq https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 &&\
    chmod +x /usr/bin/jq
RUN wget -O /tmp/packer.zip https://releases.hashicorp.com/packer/1.5.6/packer_1.5.6_linux_amd64.zip &&\
    cd /tmp/ &&\
    unzip packer.zip &&\
    mv packer /usr/bin/
RUN git clone https://github.com/codingo/Interlace.git /tmp/interlace &&\
    cd /tmp/interlace &&\
    python3 setup.py install
RUN wget -O /tmp/doctl.tar.gz https://github.com/digitalocean/doctl/releases/download/v1.45.0/doctl-1.45.0-linux-amd64.tar.gz &&\
    tar -xvzf /tmp/doctl.tar.gz &&\
    mv doctl /usr/bin/doctl
RUN curl -fsSL https://clis.cloud.ibm.com/install/linux | sh
RUN wget -O /usr/bin/gowitness https://github.com/sensepost/gowitness/releases/download/2.2.0/gowitness-2.2.0-linux-amd64 &&\
    chmod +x /usr/bin/gowitness
RUN echo "DefaultLimitNOFILE=65535" >> /etc/systemd/user.conf &&\
	echo "DefaultLimitNOFILE=65535" >> /etc/systemd/system.conf &&\
	echo "$USER hard nofile 65535" | tee -a /etc/security/limits.conf > /dev/null &&\
    echo "$USER soft nofile 65535" | tee -a /etc/security/limits.conf > /dev/null &&\
    echo "root hard nofile 65535" | tee -a /etc/security/limits.conf > /dev/null &&\
    echo "root soft nofile 65535" | tee -a /etc/security/limits.conf > /dev/null
RUN wget https://golang.org/dl/go1.14.4.linux-amd64.tar.gz &&\
    tar -xvf go1.14.4.linux-amd64.tar.gz &&\
    mv go /usr/local &&\
    export GOROOT=/usr/local/go &&\
    export GOPATH=$HOME/go &&\
    export PATH=$GOPATH/bin:$GOROOT/bin:$PATH &&\
    echo 'export GOROOT=/usr/local/go' >>~/.bash_profile &&\
    echo 'export GOPATH=$HOME/go' >>~/.bash_profile &&\
    echo 'export PATH=$GOPATH/bin:$GOROOT/bin:$PATH' >>~/.bash_profile &&\
    /bin/bash -c "source ~/.bash_profile"
ENV AXIOM_PATH="/root/.axiom"
RUN mkdir ${AXIOM_PATH}
WORKDIR ${AXIOM_PATH}
RUN echo "export PATH=\"\$PATH:${AXIOM_PATH}/interact\"" >>~/.bashrc
RUN apt install -y bc