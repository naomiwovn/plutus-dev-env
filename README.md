# Now includes Archlinux docker container with archlinux-nix

Build local
```
cd archlinux
docker build . archlinux-plutus
```

Archlinux-Plutus
```
docker run -it archlinux-plutus
cd /opt/plutus
nix-shell
cd /opt/plutus-pioneer-program
cabal update
cabal build all
```

New version includes this in the Dockerfile
```
cd /opt/plutus-pioneer-program
cabal update
cabal build all
```



Plutus-Pioneer-Program
```

## Imported from nstankov-bg/ppp 

NOTE: This repo was for cohort 1. The pattern can probably continue to be followed. Check `Issues` and `Pull requests` to see if there are changes in case this repo seems to be broken. I will also point out https://github.com/nstankov-bg/ppp as a fork for cohort 2.

Plutus Pioneers Program - Playground

The dockerfiles are current for the right plutus commit for Week06 homework. I'll try to keep it up-to-date.

## Build locally

```
docker-compose up
```

## Week 1 and 2

```
docker-compose -f docker-compose-week01.yml up
```

## Week 3

```
docker-compose -f docker-compose-week03.yml up
```

etc.
