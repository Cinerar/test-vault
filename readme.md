# Test "production-like" installation of Vault and Goldfish

These are files needed to quickly set up a test instance of [Vault](https://www.vaultproject.io)/[Goldfish](https://github.com/Caiyeon/goldfish) in production mode (that is not in "Dev" mode).

You will need to own a domain and be able to point this domain to the ip address of the machine you are running this setup on.

It uses:

- [Official Vault contailer](https://hub.docker.com/_/vault/)
- In the absence of official Goldfish container [an unofficial one](http://bla)
- [Official Traefic container](https://hub.docker.com/_/traefik/) for [Let's Encrypt](https://letsencrypt.org/) integration

This repo puts up vault / goldfish ssh protected, with TLS certs generated by Traefic via Let's Encrpt.

Settings you will need to proivde:

- EMAIL="mail@domain.tld" - email that goes to Let's Encrypt for the domain registration. This is used by Let's Encrypt for certificate revocation latter if needed.
- VAULT="vault.domain.tld" - your vault domain
- GOLDFISH="goldfish.domain.tld" - your goldfish domain

Steps to get this up and running:

- Point yout domain for vault and your domain for goldfish to the ip of the docker host machine you are going to install it to. The ip needs to be publicly available so that Let's Encrypt could validate that you own the domains.
- Clone the repo
- Copy `settings.sh.template` to `settings.sh`
- Edit settings.sh providing the settings above
- Run `init.sh` to create docker-compose.yml and traefik.toml from templates and to use them to create the docker containers

Use docker logs to diagnose if something went wrong. You should be able to go to your <https://vault.domain.tld> and <https://goldfish.domain.tld> (port 443 both) to access these. Vault naturally will give you 404 at this address.
Neither Vault nor Goldfish will be initialized. You will need to do this separately to suite your needs as per their respective documentations:

- [Vault](https://www.vaultproject.io/intro/getting-started/deploy.html#initializing-the-vault)
- [Goldfish](https://github.com/Caiyeon/goldfish/wiki/Production-Deployment#1-write-goldfish-approle)

This repository was create to test [Automatic Unseal Script](https://github.com/andrewsav-datacom/vault-unseal) for Vaut/Goldfish. There is an [example script](https://github.com/andrewsav-datacom/vault-unseal/blob/master/example-init.sh) for intializing Vault/Goldfish in the previous link.
