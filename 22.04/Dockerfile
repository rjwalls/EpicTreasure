############################################################
# Dockerfile to build Epictreasure container
# Based on Ubuntu
############################################################

FROM ubuntu:22.04
ENV test false
MAINTAINER Maintainer Robert Walls 

RUN apt-get update && \
    apt-get -y install locales

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8     

RUN mkdir -p /root/tools

RUN apt-get update && \
    apt-get -y install python2 python2-dev python-pip && \
    apt-get -y install python3 python3-dev python3-pip && \
    apt-get clean

RUN apt-get -y install man

RUN apt-get update && \
    apt-get install --no-install-recommends -y build-essential curl gdb \
    gdb-multiarch gdbserver git \
    libncursesw5-dev python3-setuptools python-setuptools \
    tree stow virtualenvwrapper \
    wget vim unzip \
    libjpeg8 libjpeg62-dev libfreetype6 libfreetype6-dev \
    squashfs-tools zlib1g-dev liblzma-dev cmake \
    z3 net-tools strace ltrace \
    gcc-multilib g++-multilib ruby-full binutils-mips-linux-gnu sudo


# Upgrade pip 
RUN python3 -m pip install --upgrade pip && \
    pip3 install ipython

# Install seccomp-tools
RUN apt-get -y install gcc ruby-dev && \
    gem install seccomp-tools

# Install pwntools and pwndbg
RUN apt-get update && \
    apt-get -y install python3 python3-pip python3-dev git libssl-dev libffi-dev build-essential && \
    python3 -m pip install --upgrade pip && \
    python3 -m pip install --upgrade pwntools

RUN cd /root/tools && \
    git clone --depth 1 https://github.com/pwndbg/pwndbg && \
    cd pwndbg && \
    ./setup.sh

# Install 32bit dependencies
RUN dpkg --add-architecture i386 && \
    apt update && \
    apt --no-install-recommends -y install libc6:i386 libncurses5:i386 libstdc++6:i386 libc6-dev-i386 && \
    apt clean

# Install apktool
RUN apt update && \
    apt install --no-install-recommends -y default-jre && \
    wget https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool && \
    wget https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.0.2.jar && \
    mv apktool_2.0.2.jar /bin/apktool.jar && \
    mv apktool /bin/ && \
    chmod 755 /bin/apktool && \
    chmod 755 /bin/apktool.jar
    
# Install PIL 
RUN pip install Pillow 

# Install frida and the frida tools
RUN pip install frida frida-tools

# Install ROPgadget
RUN python3 -m pip install ROPgadget

# Install fzf
RUN cd /root/tools && \
    git clone --depth 1 https://github.com/junegunn/fzf.git /root/.fzf && \
    /root/.fzf/install --all --key-bindings --completion 

RUN apt-get update && \
    apt-get install --no-install-recommends -y software-properties-common

# Install qemu with multiarchs
RUN apt --no-install-recommends -y install qemu qemu-user qemu-user-static && \
    apt -m update && \
    apt install -y libc6-arm64-cross libcc6-dev-i386 \
    libc6-i386 libffi-dev libssl-dev libncurses5-dev && \
    apt --no-install-recommends -y install 'binfmt*' && \
    apt --no-install-recommends -y install libc6-armhf-armel-cross && \
    apt --no-install-recommends -y install debian-keyring && \
    apt --no-install-recommends -y install debian-archive-keyring && \
    apt --no-install-recommends -y install emdebian-archive-keyring && \
    apt -m update; echo 0 && \
    apt --no-install-recommends -y install libc6-mipsel-cross && \
    apt --no-install-recommends -y install libc6-armel-cross libc6-dev-armel-cross && \
    apt --no-install-recommends -y install libc6-dev-armhf-cross && \
    apt --no-install-recommends -y install binutils-arm-linux-gnueabi && \
    apt --no-install-recommends -y install libncurses5-dev && \
    mkdir /etc/qemu-binfmt && \
    ln -s /usr/mipsel-linux-gnu /etc/qemu-binfmt/mipsel && \
    ln -s /usr/arm-linux-gnueabihf /etc/qemu-binfmt/arm && \
    apt clean

# Install Rust
RUN wget https://sh.rustup.rs && \
    chmod +x index.html && \
    ./index.html --default-toolchain nightly -y && \
    rm index.html

# Install ripgrep from Releases
RUN curl -LO https://github.com/BurntSushi/ripgrep/releases/download/13.0.0/ripgrep_13.0.0_amd64.deb && \
    dpkg -i ripgrep_13.0.0_amd64.deb && \
    rm ripgrep_13.0.0_amd64.deb

# Install one_gadget
RUN gem install one_gadget

# Install arm_now
RUN apt update && \
    apt install e2tools && \
    pip3 install https://github.com/nongiach/arm_now/archive/master.zip --upgrade && \
    apt clean



# Install DrMemory
RUN cd /root/tools && \
    wget https://github.com/DynamoRIO/drmemory/releases/download/release_1.11.0/DrMemory-Linux-1.11.0-2.tar.gz && \
    tar zxvf DrMemory* && \
    cd DrMemory* && \
    ln -s $PWD/bin/drmemory /usr/bin/drmemory-32 && \
    ln -s $PWD/bin64/drmemory /usr/bin/drmemory-64

# Install DynamoRIO
RUN cd /root/tools && \
    wget https://github.com/DynamoRIO/dynamorio/releases/download/cronbuild-7.91.18058/DynamoRIO-x86_64-Linux-7.91.18058-0.tar.gz && \
    tar zxvf DynamoRIO*tar.gz && \
    rm DynamoRIO*tar.gz && \
    wget https://github.com/DynamoRIO/dynamorio/releases/download/cronbuild-7.91.18058/DynamoRIO-i386-Linux-7.91.18058-0.tar.gz && \
    tar zxvf DynamoRIO*tar.gz && \
    rm DynamoRIO*tar.gz 

# Install Valgrind
Run apt update && \
    apt install valgrind && \
    apt clean

RUN cd /root/tools && \
    git clone --depth 1 https://github.com/ReFirmLabs/binwalk && \
    cd binwalk && \
    python3 setup.py install

# Install fmk
# RUN cd /root/tools && \
    # wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/firmware-mod-kit/fmk_099.tar.gz && \
    # tar zxvf fmk_099.tar.gz && \
    # rm fmk_099.tar.gz && \
    # cd fmk/src && \
    # ./configure && \
    # make

# Install angr
RUN python3 -m pip install angr

# Install Rust binaries
RUN /root/.cargo/bin/cargo install ripgrep exa bat

# Install gef but keep pwndbg downloaded
RUN wget -O ~/.gdbinit-gef.py -q https://gef.blah.cat/py && \
    echo source ~/.gdbinit-gef.py > ~/.gdbinit && \
    python3 -m pip install ropper
RUN wget -O ~/.gdbinit-gef-extras.sh -q https://raw.githubusercontent.com/hugsy/gef/master/scripts/gef-extras.sh && \
    chmod +x ~/.gdbinit-gef-extras.sh && \
    ~/.gdbinit-gef-extras.sh

# Install go
RUN wget https://dl.google.com/go/go1.12.6.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go*tar.gz 


# Install tmux
RUN apt-get -y install tmux


WORKDIR /root/tools

# Install radare
RUN git clone --depth 1 https://github.com/radare/radare2 && \
    cd radare2 && \
    ./sys/install.sh && \
    python3 -m pip install r2pipe


# Install keystone and python bindings
RUN git clone --depth 1 https://github.com/keystone-engine/keystone && \
    mkdir keystone/build && \
    cd keystone/build && \
    ../make-share.sh && \
    make install && \
    ldconfig  && \
    python3 -m pip install keystone-engine 

# Install unicorn and python bindings
RUN git clone --depth 1 https://github.com/unicorn-engine/unicorn && \
    mkdir unicorn/build && \
    cd unicorn/build && \
    cmake .. -DCMAKE_BUILD_TYPE=Release && \
    make && \
    cd ../bindings/python  && \
    python3 setup.py install 

# Install capstone and python bindings
RUN git clone --depth 1 https://github.com/capstone-engine/capstone && \
    cd capstone && \
    ./make.sh && \
    ./make.sh install && \
    python3 -m pip install capstone 

RUN apt-get -y install file

# Personal dotfiles
#RUN cd /root && \
#    rm .bashrc && \
#    git clone --recursive --depth 1 https://github.com/rjwalls/dotfiles.git && \
#    cd dotfiles && \
#    ./install.sh


COPY tmux.conf /root/.tmux.conf
COPY test.sh /root/test.sh
RUN chmod u+x /root/test.sh 

CMD sh -c 'if [ "$test" = true ]; then echo "Running tests"; chmod +x /root/test.sh; /root/test.sh; else /bin/bash; fi'
