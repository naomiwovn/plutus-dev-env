# Now includes Archlinux docker container with archlinux-nix
Still running into the following errors
After running 
```
archlinux-nix bootsrap
```
```
#15 38.39 Adding build-sandbox-paths to /etc/nix/nix.conf ...
#15 38.40 Enabling sandboxing ...
#15 38.41 Killing daemon ...
#15 38.41 System has not been booted with systemd as init system (PID 1). Can't operate.
#15 38.41 Failed to connect to bus: Host is down
#15 38.43 System has not been booted with systemd as init system (PID 1). Can't operate.
#15 38.43 Failed to connect to bus: Host is down
#15 38.43 Loading nix-daemon into systemd ...
#15 38.44 System has not been booted with systemd as init system (PID 1). Can't operate.
#15 38.44 Failed to connect to bus: Host is down
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
