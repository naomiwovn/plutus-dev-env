FROM archlinux

RUN pacman -Syu --noconfirm && \
    pacman -S ghc git cabal-install curl sudo systemd nix --noconfirm
RUN cabal update --ghc --dynlibdir=/opt/ghcdynlibs \
    --enable-library-vanilla --enable-executable-dynamic --enable-library-for-ghci -v

RUN pacman -S --needed base-devel --noconfirm 

# makepkg requires non-root user AND requires a password for sudoers
# Make new user and remove password requirements
RUN useradd -G wheel --no-create-home --shell=/bin/false pioneer && usermod -L pioneer 
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN echo "root ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN git clone https://aur.archlinux.org/archlinux-nix.git
RUN chown pioneer archlinux-nix && pwd && ls -al
USER pioneer
RUN cd archlinux-nix && makepkg -i --noconfirm
USER root

# Nix gives systemd error for archlinux
# Build groups and bootstrap system
RUN archlinux-nix setup-build-group
RUN archlinux-nix bootstrap

RUN nix-channel --add https://nixos.org/channels/nixpkgs-unstable
RUN nix-channel --update
RUN nix-env -u 

# after first install and before rebooting, activate nix in each new shell
RUN source /etc/profile.d/nix{,-daemon}.sh
RUN echo $PATH 

RUN mkdir /etc/nix
RUN echo "substituters        = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/" >> /etc/nix/nix.conf
RUN echo "trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=" >> /etc/nix/nix.conf

RUN chmod 777 /etc/nix/nix.conf
RUN echo "sandbox = false \
use-sqlite-wal = false \
system-feature = kvm " >> /etc/nix/nix.conf

WORKDIR /opt
RUN git clone https://github.com/input-output-hk/plutus-pioneer-program /opt/plutus-pioneer-program &&\
    cd plutus-pioneer-program

WORKDIR /opt/plutus-pioneer-program
RUN cd /opt/plutus-pioneer-program/code/week01