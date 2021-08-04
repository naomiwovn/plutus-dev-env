# Archlinux docker container with archlinux-nix
Archlinux-Plutus

Build locally
```
cd archlinux
docker build . archlinux-plutus
docker run -it archlinux-plutus
```
Or 

Docker Hub
```
docker run -it naomiwovn/archlinux-plutus:latest
```

Now you can repl into things and do the sorcery Lars did when he used 
```
cabal repl
import Ledger.TimeSlot
slotToPOSIXTime 10
```
within the /plutus-pioneer-program/code/week01 to get the POSITX Time for week01
https://www.youtube.com/watch?v=_zr3W8cgzIQ&t=3156s


Note: might need to fix excess installations of nix/archlinux-nix etc. I did that to bypass systemd errors and don't yet fully understand what breaks/fixes this for Archlinux and Nix. 

Part 2 
## Imported from nstankov-bg/ppp Plutus-Playground

Runs the playground so you can paste code and test the cool stuff you did (wrong)

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
