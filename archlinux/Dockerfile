FROM archlinux

RUN pacman -Syu --noconfirm && \
    pacman -S ghc git cabal-install --noconfirm
RUN cabal update 
RUN ghc-pkg check
    
WORKDIR /opt
RUN git clone https://github.com/input-output-hk/plutus-pioneer-program /opt/plutus-pioneer-program &&\
    cd plutus-pioneer-program

ARG WEEKONE = /opt/plutus-pioneer-program/code/week01
WORKDIR /opt/plutus-pioneer-program
RUN cd ${WEEKONE}