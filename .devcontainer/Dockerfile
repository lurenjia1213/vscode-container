FROM ubuntu:noble
ENV LANG="C.UTF-8"
ENV SHELL=/bin/bash

RUN sed -i -e 's@//.*archive.ubuntu.com@//mirrors.hust.edu.cn@g' -e 's/security.ubuntu.com/mirrors.ustc.edu.cn/g'\
/etc/apt/sources.list.d/ubuntu.sources
#如果失败，请注释上面的东西，避免被速率限制
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends  \
    build-essential llvm lldb clangd lld cppcheck valgrind cmake \
    fakeroot bison flex ccache\
    libncurses-dev libssl-dev libunwind8 libncurses6 libncursesw6 libelf-dev zlib1g-dev openssl libstdc++6 libc6 swig\
    ca-certificates\
    wget htop git-lfs git tar unzip uuid-dev tmux nano vim screen  jq bc rsync sudo wget curl\
    python-is-python3 python3-pip  python3-venv python3-dev\
    qemu-system-misc qemu-system-x86\
    gdb gdb-multiarch\
    && apt-get upgrade -y \
    && apt-get clean -y && apt-get autoremove -y &&rm -rf /var/lib/apt/lists/*\
    && sed -i 's/http:/https:/g' /etc/apt/sources.list.d/ubuntu.sources\
    &&useradd -m -s /bin/bash dev && usermod -aG sudo dev&&echo 'dev ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

##################################################################################################
USER dev
WORKDIR /home/dev/

####################################################################################################
RUN RUSTUP_DIST_SERVER="https://mirrors.hust.edu.cn/rustup" \
    RUSTUP_UPDATE_ROOT="https://mirrors.hust.edu.cn/rustup/rustup" \
    curl -sSf https://mirrors.hust.edu.cn/rustup/rustup.sh | sh -s -- --default-toolchain stable -y\
    &&pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
COPY --chown=dev:dev ./cargo_config /home/dev/.cargo/config
CMD ["sleep","infinity"]