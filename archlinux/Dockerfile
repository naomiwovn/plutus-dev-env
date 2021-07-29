FROM archlinux


ENV PIONEERPATH = "/home/pioneer/plutus-pioneer-program"
# RUN pacman -Syu --noconfirm && \
#     pacman -S ghc git cabal-install curl sudo systemd go --noconfirm

RUN pacman -Syu --noconfirm && \
    pacman -S --needed base-devel --noconfirm  && \
    pacman -S git curl sudo systemd go --noconfirm

# RUN cabal update --ghc --dynlibdir=/opt/ghcdynlibs \
#     --enable-library-vanilla --enable-executable-dynamic --enable-library-for-ghci -v

# RUN curl --proto '=https' --tlsv1.2 -sSf https://nixos.org/nix/install -o nix-install.sh
# RUN chmod +x ./nix-install.sh && ./nix-install.sh --daemon

# makepkg requires non-root user AND requires a password for sudoers
# Make new user and remove password requirements
RUN useradd -m -G wheel pioneer 
RUN echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN echo "root ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

RUN git clone https://aur.archlinux.org/yay.git
RUN chown pioneer yay && pwd && ls -al
USER pioneer 
RUN cd yay && makepkg -i -A --noconfirm

RUN yay -S archlinux-nix --noconfirm
RUN yay -S nix --noconfirm

# RUN git clone https://aur.archlinux.org/archlinux-nix.git
# RUN chown pioneer archlinux-nix && pwd && ls -al
# USER pioneer
# RUN cd archlinux-nix && makepkg -i --noconfirm

USER root
# Plutus
WORKDIR /opt
ARG PLUTUS_GIT_COMMIT=ea0ca4e9f9821a9dbfc5255fa0f42b6f2b3887c4
RUN git clone https://github.com/input-output-hk/plutus /opt/plutus && \
	cd /opt/plutus && \
	git checkout ${PLUTUS_GIT_COMMIT}

RUN nix-channel --add https://nixos.org/channels/nixpkgs-unstable
RUN nix-channel --update
RUN nix-env -u 

WORKDIR /opt/plutus
RUN chmod 777 /opt/plutus && cd /opt/plutus 
RUN nix build -f default.nix plutus.haskell.packages.plutus-core

# avoid building ghc
RUN chmod 777 /etc/nix/nix.conf
RUN echo "substituters        = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/" >> /etc/nix/nix.conf
RUN echo "trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=" >> /etc/nix/nix.conf
RUN echo -e "sandbox = false" >> /etc/nix/nix.conf
RUN echo -e "use-sqlite-wal = false" >> /etc/nix/nix.conf

USER pioneer 
# Plutus Pioneer Program
WORKDIR /home/pioneer
RUN git clone https://github.com/input-output-hk/plutus-pioneer-program PIONEERPATH

# still builds ghc ... add redundant nix.conf files :D 
RUN mkdir -p ~/.config/nix
RUN echo 'substituters = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/' >> ~/.config/nix/nix.conf
RUN echo 'trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=' >> ~/.config/nix/nix.conf
RUN echo -e "sandbox = false" >> ~/.config/nix/nix.conf
RUN echo -e "use-sqlite-wal = false" >> ~/.config/nix/nix.conf

# after first install and before rebooting, activate nix in each new shell
RUN source /etc/profile.d/nix{,-daemon}.sh
RUN cd PIONEERPATH
# build
# WORKDIR /opt/plutus
# RUN nix-shell
# RUN cd /opt/plutus-pioneer-program/code/week01
# RUN cabal update
# RUN cabal build all 